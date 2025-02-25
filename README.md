# Spiritual-Gifts-Test
Gifts of the Spirit Test

Overview

The Gifts of the Spirit Test is a simple web-based questionnaire that allows users to assess their spiritual gifts by rating a series of statements. The test dynamically generates questions, collects user responses, and calculates the top five spiritual gifts based on their selections.

Features

Dynamically generates spiritual gifts questions.

Allows users to rate statements on a scale from 1 to 5.

Stores and calculates the total score for each gift.

Displays the top five spiritual gifts based on user responses.

Provides a visually appealing UI with interactive radio buttons.

Technologies Used

HTML: For structuring the webpage.

CSS: For styling elements and making the UI user-friendly.

JavaScript: For dynamically generating questions, handling user input, and calculating results.

How It Works

Question Generation:

The test contains an array of questions, each associated with a specific spiritual gift.

Each question is presented with five rating options (1 = Lowest, 5 = Highest).

User Interaction:

Users select a rating for each statement.

Selected ratings visually update with a green background to indicate selection.

Submission & Results Calculation:

Upon clicking the Submit button, the test calculates scores by summing up the selected ratings for each spiritual gift.

The top five gifts with the highest scores are displayed in a results section.

Installation & Usage

No installation is required. Simply open the index.html file in a browser to start the test.

Running Locally

Clone or download this repository.

Open index.html in any modern web browser (Chrome, Firefox, Edge, etc.).

Answer all the questions by selecting a rating from 1 to 5.

Click the Submit button to view your top five spiritual gifts.

Customization

Editing the Question Set

To modify the questions, edit the questions array in the JavaScript section:

const questions = [
    { code: "Q56", gift: "Word of Knowledge", text: "I often recognize biblical patterns and themes others overlook." },
    { code: "Q92", gift: "Discernment", text: "I often discern when someone’s teachings are false or misleading." },
    // Add or remove questions as needed
];

Changing Styling

You can update the CSS styles within the <style> section of the HTML file to customize the look and feel of the test.

Known Issues & Fixes

Issue: No results appear after submission.

Fix: Ensure at least one question is answered before clicking submit.

Issue: The test doesn't display properly on smaller screens.

Fix: Add responsive styles using media queries for mobile-friendly design.

License

This project is open-source and available under the MIT License.

Author

Developed by [Your Name] - Feel free to contribute and improve the project!

