# -Hospital-Management-System

package HotelManagementSystem;

import java.sql.*;

public class Doctors {
    private Connection connection;

    public Doctors(Connection connection) {
        this.connection = connection;
    }

    public void viewDoctors() {
        String query = "SELECT * FROM doctors";
        try (PreparedStatement preparedStatement = connection.prepareStatement(query);
             ResultSet resultSet = preparedStatement.executeQuery()) {

            if (!resultSet.isBeforeFirst()) { // Check if there are any results
                System.out.println("No doctors found.");
                return;
            }

            System.out.println("Doctors: ");
            System.out.println("+------------+--------------------+---------------------+");
            System.out.println("| Doctor Id  | Name               | Specialization      |");
            System.out.println("+------------+--------------------+---------------------+");
            while (resultSet.next()) {
                int id = resultSet.getInt("id");
                String name = resultSet.getString("name");
                String specialization = resultSet.getString("specialization");
                System.out.printf("| %-10s | %-18s | %-20s |\n", id, name, specialization);
                System.out.println("+------------+--------------------+---------------------+");
            }
        } catch (SQLException e) {
            System.err.println("Error viewing doctors: " + e.getMessage());
            e.printStackTrace();
        }
    }

    public boolean getDoctorsById(int doctorId) {
        String query = "SELECT COUNT(*) FROM doctors WHERE id = ?";
        try (PreparedStatement preparedStatement = connection.prepareStatement(query)) {
            preparedStatement.setInt(1, doctorId);
            ResultSet resultSet = preparedStatement.executeQuery();
            boolean exists = resultSet.next() && resultSet.getInt(1) > 0; // Return true if doctor exists
            System.out.println("Checking Doctor ID: " + doctorId + " - Exists: " + exists);
            return exists;
        } catch (SQLException e) {
            System.err.println("Error checking doctor by ID: " + e.getMessage());
            return false; // Return false if an error occurs
        }
    }
}



package HotelManagementSystem;

import java.sql.*;
import java.util.Scanner;

public class Patient {
    private Connection connection;
    private Scanner scanner;

    public Patient(Connection connection, Scanner scanner) {
        this.connection = connection;
        this.scanner = scanner;
    }

    public void addPatient() {
        System.out.print("Enter Patient Name: ");
        String name = scanner.next();
        System.out.print("Enter Patient Age: ");
        int age = scanner.nextInt();
        if (age < 0) {
            System.out.println("Age cannot be negative.");
            return;
        }
        System.out.print("Enter Patient Gender: ");
        String gender = scanner.next();

        String query = "INSERT INTO patients(name, age, gender) VALUES(?, ?, ?)";
        try (PreparedStatement preparedStatement = connection.prepareStatement(query)) {
            preparedStatement.setString(1, name);
            preparedStatement.setInt(2, age);
            preparedStatement.setString(3, gender);
            int affectedRows = preparedStatement.executeUpdate();
            if (affectedRows > 0) {
                System.out.println("Patient Added Successfully!!");
            } else {
                System.out.println("Failed to add Patient!!");
            }
        } catch (SQLException e) {
            System.out.println("Error adding patient: " + e.getMessage());
        }
    }

    public void viewPatients() {
        String query = "SELECT * FROM patients";
        try (PreparedStatement preparedStatement = connection.prepareStatement(query);
             ResultSet resultSet = preparedStatement.executeQuery()) {

            System.out.println("Patients: ");
            System.out.println("+------------+--------------------+----------+------------+");
            System.out.println("| Patient Id | Name               | Age      | Gender     |");
            System.out.println("+------------+--------------------+----------+------------+");

            while (resultSet.next()) {
                int id = resultSet.getInt("id");
                String name = resultSet.getString("name");
                int age = resultSet.getInt("age");
                String gender = resultSet.getString("gender");
                System.out.printf("| %-10s | %-18s | %-8s | %-10s |\n", id, name, age, gender);
                System.out.println("+------------+--------------------+----------+------------+");
            }
        } catch (SQLException e) {
            System.out.println("Error retrieving patients: " + e.getMessage());
        }
    }

    public boolean getPatientById(int id) {
        String query = "SELECT * FROM patients WHERE id = ?";
        try (PreparedStatement preparedStatement = connection.prepareStatement(query)) {
            preparedStatement.setInt(1, id);
            ResultSet resultSet = preparedStatement.executeQuery();
            boolean exists = resultSet.next();
            System.out.println("Checking Patient ID: " + id + " - Exists: " + exists);
            return exists;
        } catch (SQLException e) {
            System.out.println("Error checking patient ID: " + e.getMessage());
        }
        return false;
    }
}



package HotelManagementSystem;

import java.sql.*;

public class Doctors {
    private Connection connection;

    public Doctors(Connection connection) {
        this.connection = connection;
    }

    public void viewDoctors() {
        String query = "SELECT * FROM doctors";
        try (PreparedStatement preparedStatement = connection.prepareStatement(query);
             ResultSet resultSet = preparedStatement.executeQuery()) {

            if (!resultSet.isBeforeFirst()) { // Check if there are any results
                System.out.println("No doctors found.");
                return;
            }

            System.out.println("Doctors: ");
            System.out.println("+------------+--------------------+---------------------+");
            System.out.println("| Doctor Id  | Name               | Specialization      |");
            System.out.println("+------------+--------------------+---------------------+");
            while (resultSet.next()) {
                int id = resultSet.getInt("id");
                String name = resultSet.getString("name");
                String specialization = resultSet.getString("specialization");
                System.out.printf("| %-10s | %-18s | %-20s |\n", id, name, specialization);
                System.out.println("+------------+--------------------+---------------------+");
            }
        } catch (SQLException e) {
            System.err.println("Error viewing doctors: " + e.getMessage());
            e.printStackTrace();
        }
    }

    public boolean getDoctorsById(int doctorId) {
        String query = "SELECT COUNT(*) FROM doctors WHERE id = ?";
        try (PreparedStatement preparedStatement = connection.prepareStatement(query)) {
            preparedStatement.setInt(1, doctorId);
            ResultSet resultSet = preparedStatement.executeQuery();
            boolean exists = resultSet.next() && resultSet.getInt(1) > 0; // Return true if doctor exists
            System.out.println("Checking Doctor ID: " + doctorId + " - Exists: " + exists);
            return exists;
        } catch (SQLException e) {
            System.err.println("Error checking doctor by ID: " + e.getMessage());
            return false; // Return false if an error occurs
        }
    }
}

