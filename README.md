# Online Support System

## Description

This is a web-based support ticket management system built with Laravel. It allows guest users to submit support tickets and check their status, and it provides a platform for support agents to manage and respond to those tickets.

## Features

* **Guest Ticket Submission:** Unregistered users can submit support tickets with their name, email, phone number, and problem description.
* **Ticket Status Tracking:** Guests can check the status of their tickets using a unique reference number.
* **Agent Ticket Management:** Authenticated support agents can view, open, and reply to tickets.
* **Ticket Listing:** Agents can search tickets by customer name, and the ticket list is paginated.
* **New Ticket Highlighting:** New tickets are highlighted in the agent ticket list.
* **Email Notifications:** Customers receive an acknowledgement email upon ticket submission and a reply email when an agent responds.
* **Responsive Design:** The UI is designed to be responsive across various screen sizes (mobile, tablet, desktop).
* **Input Validation:** All inputs are validated to ensure data integrity.
* **Secure Data Handling:** The system uses Laravel's security features to protect personal data.

## Assumptions

* **Guest User Flow:**
    * Guest users are not required to create an account to submit a ticket.
    * Guest users interact with the system only to submit tickets and check their status.
* **Agent User Flow:**
    * Support agents are assumed to have accounts and log in to the system to manage tickets.
    * Agent authentication is handled by Laravel Breeze.
* **Email Configuration:**
    * It is assumed that the Laravel application is configured to send emails.  This requires setting up an email driver (e.g., SMTP, Mailgun, etc.) in the `.env` file.
* **Database Setup:**
    * A MySQL database is used. The database connection details are assumed to be correctly configured in the `.env` file.
* **Frontend:**
     * Boostrap and Tailwind CSS is used for styling.

## Improvements Done

* **Authentication:** Replaced the deprecated `make:auth` with Laravel Breeze for setting up authentication.
* **JSON API:** Implemented JSON responses for the ticket status check API.
* **Database:** Improved the database schema, including adding indexes and foreign key constraints.
* **AJAX:** Implemented AJAX for submitting replies in the agent ticket view.
* **Code Quality:** Improved code organization, readability, and adherence to Laravel best practices.
* **Error Handling:** Implemented more robust error handling, including validation and exception handling.
* **Security:** Ensured that  data is passed to views using `e()` to prevent XSS vulnerabilities.
* **Documentation:** Added a comprehensive README file.

## How to Test the Project on a New Machine

Follow these steps to set up and test the project on a new machine:

### Prerequisites

* PHP >= 8.1
* Composer
* MySQL
* Node.js and npm

### Installation

1.  **Clone the repository:**
    ```bash
    git clone <repository_url>
    cd <project_directory>
    ```

2.  **Install PHP dependencies:**
    ```bash
    composer install
    ```

3.  **Copy the `.env` file:**
    ```bash
    cp .env.example .env
    ```

4.  **Configure the `.env` file:**
    * Set up your database connection details (DB\_HOST, DB\_DATABASE, DB\_USERNAME, DB\_PASSWORD).
    * Configure your email settings (MAIL\_MAILER, MAIL\_HOST, MAIL\_PORT, MAIL\_USERNAME, MAIL\_PASSWORD, MAIL\_ENCRYPTION, MAIL\_FROM\_ADDRESS, MAIL\_FROM\_NAME).
    * Generate an application key:
        ```bash
        php artisan key:generate
        ```

5.  **Set up the database:**
    ```bash
    php artisan migrate
    ```

6.  **Install Node.js dependencies and build assets:**
    ```bash
    npm install
    npm run dev
    ```

7.  **Install Laravel Breeze for authentication:**
     ```bash
        composer require laravel/breeze --dev
        php artisan breeze:install
        php artisan migrate
    ```

8.  **Serve the application:**
    ```bash
    php artisan serve
    ```

9.  **Access the application in your browser:**
    Open your browser and go to `http://localhost:8000`.

### Testing

1.  **Submit a ticket as a guest:**
    * Go to the `/submit-ticket` route.
    * Fill in the form and submit the ticket.
    * Verify that you receive a success message with a reference number.
    * Check your email for the ticket acknowledgement.

2.  **Check ticket status as a guest:**
    * Go to the `/check-status` route.
    * Enter the reference number you received.
    * Verify that you can see the ticket status.
    * Enter an invalid reference number and verify that you get an error message.

3.  **Log in as an agent:**
    * Go to the login route (defined by Breeze, usually `/login`).
    * Log in with a valid agent account.  You might need to create a user using `php artisan tinker` and the `User::factory()->create()` command.
    * Verify that you are redirected to the agent dashboard (`/agent/dashboard`).

4.  **View and manage tickets as an agent:**
    * Go to the `/agent/tickets` route.
    * Verify that you can see a list of tickets.
    * Click on a ticket to view its details (`/agent/tickets/{id}`).
    * Reply to the ticket using the form.
    * Verify that the reply is displayed and that the customer receives an email notification.

5.  **Test API endpoints:**
     * Use a tool like Postman or `curl` to test the JSON API endpoints.
     * Test the  `/check-status`  endpoint with a valid and invalid reference number.  Verify the JSON responses and HTTP status codes.#

6.  **Email Responce:**
    * I've added MAIL_MAILER=log to the .env file configuration section. This will ensure that Laravel writes emails to the log files         instead of attempting to send them.

    **For automated testing:**
        * Create PHPUnit tests.
     * -Online-Support-System
