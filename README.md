package application;

import java.awt.event.ActionEvent;

import java.awt.event.ActionListener;



import javax.swing.BoxLayout;

import javax.swing.ButtonGroup;

import javax.swing.JButton;

import javax.swing.JFrame;

import javax.swing.JLabel;

import javax.swing.JOptionPane;

import javax.swing.JPanel;

import javax.swing.JPasswordField;

import javax.swing.JRadioButton;

import javax.swing.JTextField;

import javax.swing.SwingUtilities;



public class QuizApplication extends JFrame implements ActionListener {



    private static final long serialVersionUID = 1L;



    // Quiz data and UI components

    private JLabel questionLabel;

    private JRadioButton option1, option2, option3, option4;

    private ButtonGroup optionsGroup;

    private JButton nextButton;

    private String[][] quizData = {

            {"What is the capital of France?", "Paris", "London", "Berlin", "Madrid"},

            {"What is the largest planet in our solar system?", "Jupiter", "Saturn", "Earth", "Mars"},

            {"Who wrote 'Romeo and Juliet'?", "William Shakespeare", "Jane Austen", "Charles Dickens", "Mark Twain"}

    };

    private int currentQuestion = 0;



    // Login UI components

    private JTextField usernameField;

    private JPasswordField passwordField;

    private JButton loginButton;



    // Panels

    private JPanel loginPanel;

    private JPanel quizPanel;



    // Constructor for the quiz application

    public QuizApplication() {

        setTitle("Quiz Application");

        setSize(400, 300);

        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        setLocationRelativeTo(null);



        // Initialize login panel

        loginPanel = new JPanel();

        loginPanel.setLayout(new BoxLayout(loginPanel, BoxLayout.Y_AXIS));

        setupLoginPanel();



        // Initialize quiz panel

        quizPanel = new JPanel();

        quizPanel.setLayout(new BoxLayout(quizPanel, BoxLayout.Y_AXIS));

        setupQuizPanel();



        // Initially show login panel

        getContentPane().add(loginPanel);

        quizPanel.setVisible(false); // Hide quiz panel initially



        setVisible(true);

    }



    private void setupLoginPanel() {

        JLabel usernameLabel = new JLabel("Username:");

        loginPanel.add(usernameLabel);



        usernameField = new JTextField(20);

        loginPanel.add(usernameField);



        JLabel passwordLabel = new JLabel("Password:");

        loginPanel.add(passwordLabel);



        passwordField = new JPasswordField(20);

        loginPanel.add(passwordField);



        loginButton = new JButton("Login");

        loginButton.addActionListener(this);

        loginPanel.add(loginButton);

    }



    private void setupQuizPanel() {

        questionLabel = new JLabel();

        quizPanel.add(questionLabel);



        optionsGroup = new ButtonGroup();



        option1 = new JRadioButton();

        optionsGroup.add(option1);

        quizPanel.add(option1);



        option2 = new JRadioButton();

        optionsGroup.add(option2);

        quizPanel.add(option2);



        option3 = new JRadioButton();

        optionsGroup.add(option3);

        quizPanel.add(option3);



        option4 = new JRadioButton();

        optionsGroup.add(option4);

        quizPanel.add(option4);



        nextButton = new JButton("Next");

        nextButton.addActionListener(this);

        quizPanel.add(nextButton);

    }



    @Override

    public void actionPerformed(ActionEvent e) {

        if (e.getSource() == loginButton) {

            String enteredUsername = usernameField.getText();

            String enteredPassword = new String(passwordField.getPassword());



            if (enteredUsername.equals("admin") && enteredPassword.equals("123")) {

                // Successful login, show quiz panel

                getContentPane().remove(loginPanel); // Remove login panel

                getContentPane().add(quizPanel); // Add quiz panel

                quizPanel.setVisible(true); // Show quiz panel



                // Initialize first question

                updateQuestion();

            } else {

                JOptionPane.showMessageDialog(this, "Invalid username or password. Try again.");

                usernameField.setText("");

                passwordField.setText("");

            }

        } else if (e.getSource() == nextButton) {

            if (optionsGroup.getSelection() == null) {

                JOptionPane.showMessageDialog(this, "Please select an answer.");

                return; // Exit actionPerformed without progressing if no option is selected

            }



            String selectedAnswer = optionsGroup.getSelection().getActionCommand();

            // Add logic to check the selected answer against the correct answer if needed



            // Move to the next question

            currentQuestion++;

            if (currentQuestion < quizData.length) {

                updateQuestion();

            } else {

                JOptionPane.showMessageDialog(this, "Quiz completed!");

                System.exit(0);

            }

        }

    }



    private void updateQuestion() {

        questionLabel.setText(quizData[currentQuestion][0]);

        option1.setText(quizData[currentQuestion][1]);

        option1.setActionCommand(quizData[currentQuestion][1]);

        option2.setText(quizData[currentQuestion][2]);

        option2.setActionCommand(quizData[currentQuestion][2]);

        option3.setText(quizData[currentQuestion][3]);

        option3.setActionCommand(quizData[currentQuestion][3]);

        option4.setText(quizData[currentQuestion][4]);

        option4.setActionCommand(quizData[currentQuestion][4]);

        optionsGroup.clearSelection();

    }



    public static void main(String[] args) {

        SwingUtilities.invokeLater(new Runnable() {

            @Override

            public void run() {

                new QuizApplication();

            }

        });

    }

}