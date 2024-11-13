// Single Java Code
import java.awt.*;
import java.sql.*;
import java.util.ArrayList;
import javax.swing.*;

public class ExamSeatingArrangementSystem extends JFrame {

    private Connection conn;
    private String currentSeatingArrangement;

    public ExamSeatingArrangementSystem() {
        connectToDatabase();
        showLoginScreen();
    }

    private void connectToDatabase() {
        String url = "jdbc:mysql://localhost:3306/exam_system";
        String user = "root";
        String password = "#Dhoni@7";

        try {
            conn = DriverManager.getConnection(url, user, password);
            System.out.println("Database connected successfully!");
        } catch (SQLException e) {
            JOptionPane.showMessageDialog(this, "Failed to connect to database.");
            e.printStackTrace();
        }
    }

    private void setupMenuBar() {
        JMenuBar menuBar = new JMenuBar();
        JMenu fileMenu = new JMenu("File");
        JMenuItem logoutItem = new JMenuItem("Logout");

        logoutItem.addActionListener(e -> logout());

        fileMenu.add(logoutItem);
        menuBar.add(fileMenu);
        setJMenuBar(menuBar);
    }

    private void logout() {
        this.dispose(); // Close current window
        showLoginScreen(); // Return to login screen
    }

    private void showLoginScreen() {
        JPanel loginPanel = new JPanel();
        loginPanel.setLayout(new BoxLayout(loginPanel, BoxLayout.Y_AXIS));
        loginPanel.setBackground(Color.decode("#EDE7F6"));
        loginPanel.setBorder(BorderFactory.createEmptyBorder(50, 50, 50, 50));

        JLabel titleLabel = new JLabel("Exam Hall Seating Arrangement");
        titleLabel.setFont(new Font("Arial", Font.BOLD, 24));
        titleLabel.setAlignmentX(Component.CENTER_ALIGNMENT);
        titleLabel.setForeground(Color.decode("#6A1B9A"));

        JButton studentLoginButton = new JButton("STUDENT LOGIN");
        JButton adminLoginButton = new JButton("ADMIN LOGIN");

        studentLoginButton.setBackground(Color.decode("#6A1B9A"));
        studentLoginButton.setForeground(Color.WHITE);
        studentLoginButton.setAlignmentX(Component.CENTER_ALIGNMENT);
        studentLoginButton.setPreferredSize(new Dimension(250, 40));

        adminLoginButton.setBackground(Color.decode("#6A1B9A"));
        adminLoginButton.setForeground(Color.WHITE);
        adminLoginButton.setAlignmentX(Component.CENTER_ALIGNMENT);
        adminLoginButton.setPreferredSize(new Dimension(250, 40));

        studentLoginButton.addActionListener(e -> {
            this.dispose();
            showStudentLoginScreen();
        });

        adminLoginButton.addActionListener(e -> {
            this.dispose();
            showAdminLoginScreen();
        });

        loginPanel.add(titleLabel);
        loginPanel.add(Box.createRigidArea(new Dimension(0, 20)));
        loginPanel.add(studentLoginButton);
        loginPanel.add(Box.createRigidArea(new Dimension(0, 10)));
        loginPanel.add(adminLoginButton);

        JFrame loginFrame = new JFrame("Login");
        loginFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        loginFrame.setSize(400, 300);
        loginFrame.setLocationRelativeTo(null);
        loginFrame.setContentPane(loginPanel);
        loginFrame.setVisible(true);
    }

    private void showStudentLoginScreen() {
        JPanel studentLoginPanel = new JPanel();
        studentLoginPanel.setLayout(new BoxLayout(studentLoginPanel, BoxLayout.Y_AXIS));
        studentLoginPanel.setBackground(Color.decode("#EDE7F6"));
        studentLoginPanel.setBorder(BorderFactory.createEmptyBorder(50, 50, 50, 50));

        JLabel studentTitleLabel = new JLabel("Student Login");
        studentTitleLabel.setFont(new Font("Arial", Font.BOLD, 24));
        studentTitleLabel.setAlignmentX(Component.CENTER_ALIGNMENT);
        studentTitleLabel.setForeground(Color.decode("#6A1B9A"));

        JTextField rollNumberField = new JTextField();
        rollNumberField.setPreferredSize(new Dimension(250, 30));
        rollNumberField.setMaximumSize(rollNumberField.getPreferredSize());

        JButton loginButton = new JButton("LOGIN");
        loginButton.setBackground(Color.decode("#6A1B9A"));
        loginButton.setForeground(Color.WHITE);
        loginButton.setAlignmentX(Component.CENTER_ALIGNMENT);
        loginButton.setPreferredSize(new Dimension(250, 40));

        loginButton.addActionListener(e -> {
            String rollNumber = rollNumberField.getText();
            showStudentDashboard(rollNumber);
        });

        studentLoginPanel.add(studentTitleLabel);
        studentLoginPanel.add(Box.createRigidArea(new Dimension(0, 20)));
        studentLoginPanel.add(rollNumberField);
        studentLoginPanel.add(Box.createRigidArea(new Dimension(0, 20)));
        studentLoginPanel.add(loginButton);

        JFrame studentLoginFrame = new JFrame("Student Login");
        studentLoginFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        studentLoginFrame.setSize(400, 300);
        studentLoginFrame.setLocationRelativeTo(null);
        studentLoginFrame.setContentPane(studentLoginPanel);
        studentLoginFrame.setVisible(true);
    }

    private void showAdminLoginScreen() {
        JPanel adminLoginPanel = new JPanel();
        adminLoginPanel.setLayout(new BoxLayout(adminLoginPanel, BoxLayout.Y_AXIS));
        adminLoginPanel.setBackground(Color.decode("#EDE7F6"));
        adminLoginPanel.setBorder(BorderFactory.createEmptyBorder(50, 50, 50, 50));

        JLabel adminTitleLabel = new JLabel("Admin Login");
        adminTitleLabel.setFont(new Font("Arial", Font.BOLD, 24));
        adminTitleLabel.setAlignmentX(Component.CENTER_ALIGNMENT);
        adminTitleLabel.setForeground(Color.decode("#6A1B9A"));

        JTextField usernameField = new JTextField();
        usernameField.setPreferredSize(new Dimension(250, 30));
        usernameField.setMaximumSize(usernameField.getPreferredSize());

        JPasswordField passwordField = new JPasswordField();
        passwordField.setPreferredSize(new Dimension(250, 30));
        passwordField.setMaximumSize(passwordField.getPreferredSize());

        JButton loginButton = new JButton("LOGIN");
        loginButton.setBackground(Color.decode("#6A1B9A"));
        loginButton.setForeground(Color.WHITE);
        loginButton.setAlignmentX(Component.CENTER_ALIGNMENT);
        loginButton.setPreferredSize(new Dimension(250, 40));

        loginButton.addActionListener(e -> {
            String username = usernameField.getText();
            String password = new String(passwordField.getPassword());

            if (username.equals("admin") && password.equals("adminpassword")) {
                this.dispose();
                showAdminDashboard();
            } else {
                JOptionPane.showMessageDialog(this, "Invalid admin credentials.");
            }
        });

        adminLoginPanel.add(adminTitleLabel);
        adminLoginPanel.add(Box.createRigidArea(new Dimension(0, 20)));
        adminLoginPanel.add(usernameField);
        adminLoginPanel.add(Box.createRigidArea(new Dimension(0, 10)));
        adminLoginPanel.add(passwordField);
        adminLoginPanel.add(Box.createRigidArea(new Dimension(0, 20)));
        adminLoginPanel.add(loginButton);

        JFrame adminLoginFrame = new JFrame("Admin Login");
        adminLoginFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        adminLoginFrame.setSize(400, 300);
        adminLoginFrame.setLocationRelativeTo(null);
        adminLoginFrame.setContentPane(adminLoginPanel);
        adminLoginFrame.setVisible(true);
    }

    private void showAdminDashboard() {
        setTitle("Admin Dashboard - Manage Students & Rooms");
        setSize(600, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout());
        getContentPane().setBackground(Color.decode("#add8e6"));

        JLabel titleLabel = new JLabel("Admin Dashboard", SwingConstants.CENTER);
        titleLabel.setFont(new Font("Serif", Font.BOLD, 24));
        add(titleLabel, BorderLayout.NORTH);

        JMenuBar menuBar = new JMenuBar();
        JMenu fileMenu = new JMenu("File");
        JMenuItem logoutItem = new JMenuItem("Logout");

        logoutItem.addActionListener(e -> {
            this.dispose();
            showLoginScreen();
        });

        fileMenu.add(logoutItem);
        menuBar.add(fileMenu);
        setJMenuBar(menuBar);

        JButton manageStudentsButton = new JButton("Manage Students");
        JButton manageRoomsButton = new JButton("Manage Rooms");
        JButton seatingPlanButton = new JButton("Set Seating Plan");
        JButton viewSeatingButton = new JButton("View Seating Arrangement");

        JPanel buttonPanel = new JPanel();
        buttonPanel.setLayout(new GridLayout(1, 4, 10, 10));
        buttonPanel.setBackground(Color.decode("#add8e6"));
        buttonPanel.add(manageStudentsButton);
        buttonPanel.add(manageRoomsButton);
        buttonPanel.add(seatingPlanButton);
        buttonPanel.add(viewSeatingButton);

        add(buttonPanel, BorderLayout.CENTER);

        manageStudentsButton.addActionListener(e -> manageStudents());
        manageRoomsButton.addActionListener(e -> manageRooms());
        seatingPlanButton.addActionListener(e -> generateSeatingArrangement());
        viewSeatingButton.addActionListener(e -> viewSeatingArrangement());

        setVisible(true);
    }

    private void showStudentDashboard(String studentRollNumber) {
        setTitle("Student Dashboard - Exam Seating Plan");
        setSize(400, 300);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout());

        JLabel welcomeLabel = new JLabel("Welcome, Student " + studentRollNumber, SwingConstants.CENTER);
        welcomeLabel.setFont(new Font("Serif", Font.BOLD, 20));
        add(welcomeLabel, BorderLayout.NORTH);

        JButton viewSeatingButton = new JButton("View My Seating");
        viewSeatingButton.addActionListener(e -> {
            JOptionPane.showMessageDialog(this, "Your seating arrangement is: 21");
        });

        add(viewSeatingButton, BorderLayout.CENTER);
        setVisible(true);
    }

    private void manageStudents() {
        JPanel studentManagementPanel = new JPanel();
        studentManagementPanel.setLayout(new BoxLayout(studentManagementPanel, BoxLayout.Y_AXIS));
        studentManagementPanel.setBackground(Color.decode("#EDE7F6"));
        studentManagementPanel.setBorder(BorderFactory.createEmptyBorder(50, 50, 50, 50));

        JLabel studentManagementLabel = new JLabel("Manage Students");
        studentManagementLabel.setFont(new Font("Arial", Font.BOLD, 24));
        studentManagementLabel.setAlignmentX(Component.CENTER_ALIGNMENT);
        studentManagementLabel.setForeground(Color.decode("#6A1B9A"));

        JTextField rollNumberField = new JTextField();
        rollNumberField.setPreferredSize(new Dimension(250, 30));
        rollNumberField.setMaximumSize(rollNumberField.getPreferredSize());

        JTextField nameField = new JTextField();
        nameField.setPreferredSize(new Dimension(250, 30));
        nameField.setMaximumSize(nameField.getPreferredSize());

        JButton addStudentButton = new JButton("Add Student");
        JButton viewStudentsButton = new JButton("View Students");
        JButton deleteStudentButton = new JButton("Delete Student");

        addStudentButton.setBackground(Color.decode("#6A1B9A"));
        addStudentButton.setForeground(Color.WHITE);
        viewStudentsButton.setBackground(Color.decode("#6A1B9A"));
        viewStudentsButton.setForeground(Color.WHITE);
        deleteStudentButton.setBackground(Color.decode("#6A1B9A"));
        deleteStudentButton.setForeground(Color.WHITE);

        addStudentButton.addActionListener(e -> {
            String rollNumber = rollNumberField.getText().trim();
            String name = nameField.getText().trim();

            if (rollNumber.isEmpty() || name.isEmpty()) {
                JOptionPane.showMessageDialog(this, "Please fill in both fields.");
                return;
            }

            try {
                String query = "INSERT INTO students (roll_number, name) VALUES (?, ?)";
                PreparedStatement stmt = conn.prepareStatement(query);
                stmt.setString(1, rollNumber);
                stmt.setString(2, name);
                stmt.executeUpdate();
                JOptionPane.showMessageDialog(this, "Student added successfully!");
                rollNumberField.setText("");
                nameField.setText("");
            } catch (SQLException ex) {
                JOptionPane.showMessageDialog(this, "Error adding student: " + ex.getMessage());
            }
        });

        viewStudentsButton.addActionListener(e -> {
            try {
                String query = "SELECT * FROM students";
                Statement stmt = conn.createStatement();
                ResultSet rs = stmt.executeQuery(query);
                StringBuilder studentList = new StringBuilder("Students:\n");
                while (rs.next()) {
                    studentList.append("Roll Number: ").append(rs.getString("roll_number"))
                            .append(", Name: ").append(rs.getString("name")).append("\n");
                }
                JOptionPane.showMessageDialog(this, studentList.toString());
            } catch (SQLException ex) {
                JOptionPane.showMessageDialog(this, "Error fetching students: " + ex.getMessage());
            }
        });

        deleteStudentButton.addActionListener(e -> {
            String rollNumber = rollNumberField.getText().trim();
            if (rollNumber.isEmpty()) {
                JOptionPane.showMessageDialog(this, "Please enter a roll number.");
                return;
            }

            try {
                String query = "DELETE FROM students WHERE roll_number = ?";
                PreparedStatement stmt = conn.prepareStatement(query);
                stmt.setString(1, rollNumber);
                int affectedRows = stmt.executeUpdate();
                if (affectedRows > 0) {
                    JOptionPane.showMessageDialog(this, "Student " + rollNumber + " has been deleted.");
                } else {
                    JOptionPane.showMessageDialog(this, "No student found with the roll number " + rollNumber + ".");
                }
            } catch (SQLException ex) {
                JOptionPane.showMessageDialog(this, "Error deleting student: " + ex.getMessage());
            }
            rollNumberField.setText("");
            nameField.setText("");
        });

        studentManagementPanel.add(studentManagementLabel);
        studentManagementPanel.add(Box.createRigidArea(new Dimension(0, 20)));
        studentManagementPanel.add(new JLabel("Roll Number:"));
        studentManagementPanel.add(rollNumberField);
        studentManagementPanel.add(new JLabel("Name:"));
        studentManagementPanel.add(nameField);
        studentManagementPanel.add(Box.createRigidArea(new Dimension(0, 20)));
        studentManagementPanel.add(addStudentButton);
        studentManagementPanel.add(Box.createRigidArea(new Dimension(0, 10)));
        studentManagementPanel.add(viewStudentsButton);
        studentManagementPanel.add(Box.createRigidArea(new Dimension(0, 10)));
        studentManagementPanel.add(deleteStudentButton);

        JFrame manageStudentsFrame = new JFrame("Manage Students");
        manageStudentsFrame.setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE);
        manageStudentsFrame.setSize(400, 400);
        manageStudentsFrame.setLocationRelativeTo(null);
        manageStudentsFrame.setContentPane(studentManagementPanel);
        manageStudentsFrame.setVisible(true);
    }

    private void manageRooms() {
        JPanel roomManagementPanel = new JPanel();
        roomManagementPanel.setLayout(new BoxLayout(roomManagementPanel, BoxLayout.Y_AXIS));
        roomManagementPanel.setBackground(Color.decode("#EDE7F6"));
        roomManagementPanel.setBorder(BorderFactory.createEmptyBorder(50, 50, 50, 50));

        JLabel roomManagementLabel = new JLabel("Manage Rooms");
        roomManagementLabel.setFont(new Font("Arial", Font.BOLD, 24));
        roomManagementLabel.setAlignmentX(Component.CENTER_ALIGNMENT);
        roomManagementLabel.setForeground(Color.decode("#6A1B9A"));

        JTextField roomNumberField = new JTextField();
        roomNumberField.setPreferredSize(new Dimension(250, 30));
        roomNumberField.setMaximumSize(roomNumberField.getPreferredSize());

        JTextField capacityField = new JTextField();
        capacityField.setPreferredSize(new Dimension(250, 30));
        capacityField.setMaximumSize(capacityField.getPreferredSize());

        JButton addRoomButton = new JButton("Add Room");
        JButton viewRoomsButton = new JButton("View Rooms");
        JButton deleteRoomButton = new JButton("Delete Room");

        addRoomButton.setBackground(Color.decode("#6A1B9A"));
        addRoomButton.setForeground(Color.WHITE);
        viewRoomsButton.setBackground(Color.decode("#6A1B9A"));
        viewRoomsButton.setForeground(Color.WHITE);
        deleteRoomButton.setBackground(Color.decode("#6A1B9A"));
        deleteRoomButton.setForeground(Color.WHITE);

        addRoomButton.addActionListener(e -> {
            String roomNumber = roomNumberField.getText().trim();
            String capacityText = capacityField.getText().trim();

            if (roomNumber.isEmpty() || capacityText.isEmpty()) {
                JOptionPane.showMessageDialog(this, "Please fill in both fields.");
                return;
            }

            try {
                int capacity = Integer.parseInt(capacityText);
                String query = "INSERT INTO rooms (room_number, capacity) VALUES (?, ?)";
                PreparedStatement stmt = conn.prepareStatement(query);
                stmt.setString(1, roomNumber);
                stmt.setInt(2, capacity);
                stmt.executeUpdate();
                JOptionPane.showMessageDialog(this, "Room added successfully!");
                roomNumberField.setText("");
                capacityField.setText("");
            } catch (NumberFormatException ex) {
                JOptionPane.showMessageDialog(this, "Capacity must be a number.");
            } catch (SQLException ex) {
                JOptionPane.showMessageDialog(this, "Error adding room: " + ex.getMessage());
            }
        });

        viewRoomsButton.addActionListener(e -> {
            try {
                String query = "SELECT * FROM rooms";
                Statement stmt = conn.createStatement();
                ResultSet rs = stmt.executeQuery(query);
                StringBuilder roomList = new StringBuilder("Rooms:\n");
                while (rs.next()) {
                    roomList.append("Room Number: ").append(rs.getString("room_number"))
                            .append(", Capacity: ").append(rs.getInt("capacity")).append("\n");
                }
                JOptionPane.showMessageDialog(this, roomList.toString());
            } catch (SQLException ex) {
                JOptionPane.showMessageDialog(this, "Error fetching rooms: " + ex.getMessage());
            }
        });

        deleteRoomButton.addActionListener(e -> {
            String roomNumber = roomNumberField.getText().trim();
            if (roomNumber.isEmpty()) {
                JOptionPane.showMessageDialog(this, "Please enter a room number.");
                return;
            }

            try {
                String query = "DELETE FROM rooms WHERE room_number = ?";
                PreparedStatement stmt = conn.prepareStatement(query);
                stmt.setString(1, roomNumber);
                int affectedRows = stmt.executeUpdate();
                if (affectedRows > 0) {
                    JOptionPane.showMessageDialog(this, "Room " + roomNumber + " has been deleted.");
                } else {
                    JOptionPane.showMessageDialog(this, "No room found with the room number " + roomNumber + ".");
                }
            } catch (SQLException ex) {
                JOptionPane.showMessageDialog(this, "Error deleting room: " + ex.getMessage());
            }
            roomNumberField.setText("");
            capacityField.setText("");
        });

        roomManagementPanel.add(roomManagementLabel);
        roomManagementPanel.add(Box.createRigidArea(new Dimension(0, 20)));
        roomManagementPanel.add(new JLabel("Room Number:"));
        roomManagementPanel.add(roomNumberField);
        roomManagementPanel.add(new JLabel("Capacity:"));
        roomManagementPanel.add(capacityField);
        roomManagementPanel.add(Box.createRigidArea(new Dimension(0, 20)));
        roomManagementPanel.add(addRoomButton);
        roomManagementPanel.add(Box.createRigidArea(new Dimension(0, 10)));
        roomManagementPanel.add(viewRoomsButton);
        roomManagementPanel.add(Box.createRigidArea(new Dimension(0, 10)));
        roomManagementPanel.add(deleteRoomButton);

        JFrame manageRoomsFrame = new JFrame("Manage Rooms");
        manageRoomsFrame.setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE);
        manageRoomsFrame.setSize(400, 400);
        manageRoomsFrame.setLocationRelativeTo(null);
        manageRoomsFrame.setContentPane(roomManagementPanel);
        manageRoomsFrame.setVisible(true);
    }

    private void generateSeatingArrangement() {
        // Placeholder for seating arrangement generation logic
        currentSeatingArrangement = "Seating arrangement generated.";
        JOptionPane.showMessageDialog(this, currentSeatingArrangement);
    }

    private void viewSeatingArrangement() {
        try {
            String query = "SELECT student_id, room_number, seat_number FROM seating_arrangements ORDER BY room_number, seat_number";
            Statement stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery(query);

            StringBuilder seatingArrangement = new StringBuilder("Seating Arrangement:\n");
            while (rs.next()) {
                String studentId = rs.getString("student_id");
                String roomNumber = rs.getString("room_number");
                int seatNumber = rs.getInt("seat_number");
                seatingArrangement.append("Room: ").append(roomNumber)
                        .append(", Seat: ").append(seatNumber)
                        .append(", Student ID: ").append(studentId).append("\n");
            }

            if (seatingArrangement.length() == 0) {
                seatingArrangement.append("No seating arrangement found.");
            }

            JOptionPane.showMessageDialog(this, seatingArrangement.toString());
        } catch (SQLException ex) {
            JOptionPane.showMessageDialog(this, "Error fetching seating arrangement: " + ex.getMessage());
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new ExamSeatingArrangementSystem());
    }
}
