# Project
import java.util.*;

class Movie {
    String title;
    int totalSeats;
    int availableSeats;

    public Movie(String title, int totalSeats) {
        this.title = title;
        this.totalSeats = totalSeats;
        this.availableSeats = totalSeats;
    }

    public boolean bookSeats(int count) {
        if (count <= availableSeats) {
            availableSeats -= count;
            return true;
        }
        return false;
    }

    public void displayInfo() {
        System.out.println("Movie: " + title + " | Available Seats: " + availableSeats);
    }
}

public class MovieTicketBookingSystem {
    static Scanner scanner = new Scanner(System.in);
    static List<Movie> movies = new ArrayList<>();

    public static void main(String[] args) {
        // Add sample movies
        movies.add(new Movie("Avengers: Endgame", 50));
        movies.add(new Movie("Inception", 40));
        movies.add(new Movie("The Dark Knight", 30));

        int choice;

        do {
            System.out.println("\n=== Movie Ticket Booking System ===");
            System.out.println("1. View Movies");
            System.out.println("2. Book Tickets");
            System.out.println("3. Exit");
            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();
            scanner.nextLine(); // consume newline

            switch (choice) {
                case 1:
                    displayMovies();
                    break;
                case 2:
                    bookTickets();
                    break;
                case 3:
                    System.out.println("Thank you for using the Movie Ticket Booking System!");
                    break;
                default:
                    System.out.println("Invalid choice. Try again.");
            }

        } while (choice != 3);
    }

    static void displayMovies() {
        System.out.println("\n--- Available Movies ---");
        for (int i = 0; i < movies.size(); i++) {
            System.out.print((i + 1) + ". ");
            movies.get(i).displayInfo();
        }
    }

    static void bookTickets() {
        displayMovies();
        System.out.print("Select movie number to book: ");
        int movieIndex = scanner.nextInt() - 1;

        if (movieIndex < 0 || movieIndex >= movies.size()) {
            System.out.println("Invalid movie selection.");
            return;
        }

        System.out.print("Enter number of tickets: ");
        int count = scanner.nextInt();

        Movie selectedMovie = movies.get(movieIndex);
        if (selectedMovie.bookSeats(count)) {
            System.out.println("Booking successful! Enjoy the show.");
        } else {
            System.out.println("Not enough seats available.");
        }
    }
}
