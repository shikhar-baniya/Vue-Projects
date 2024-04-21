## Simple Todo List App Docs

## Table of Contents

1. [Introduction](#1-introduction)
2. [Project Overview](#2-project-overview)
3. [Getting Started](#3-getting-started)
4. [Code Structure](#4-code-structure)
5. [Dependencies](#5-dependencies)
6. [Usage](#8-usage)
7. [License](#9-license)

## 1. Introduction

Welcome to the documentation for the TodoZen App, a simple and refactored project designed to manage your tasks efficiently. This document provides an overview of the project, its code structure, refactoring details, deployment information, and usage instructions.

## 2. Project Overview

The TodoZen App is a web-based application developed in Vue.js to help users manage their tasks by providing a user-friendly interface for adding, editing, and deleting tasks. The app also supports task filtering based on status (All, Pending, Completed) and incorporates a theme switcher for a personalized user experience.

## 3. Getting Started

To get started with the TodoZen App, follow these steps:

### Prerequisites

Make sure you have the following installed:

- A modern web browser (e.g., Chrome, Firefox, Safari)
- A Code Editor (e.g., VS Code, Atom, etc.)
- Node installed om your Machine.
- An internet connection (for fetching external dependencies)

### Installation

1. **Clone the Repository:**

   ```bash
   git clone git@github.com:shikhar-baniya/Vue-Projects.git
   ```

2. **Open the folder on your Code Editor**
3. **Open Terminal and Navigate to the Project Directory:**

   ```bash
   cd todo-app
   ```

4. **Run the following command:**
   ```bash
   npm run serve
   ```

   This will run the app on your local server on 8080 port.


## 4. Code Structure

The project follows a modular and organized structure to enhance readability, maintainability, and scalability. Since this is a Vue Project, we are using vue components and project structure to improve the efficiency of the code. Key components include:

- **App.vue:** The main structure of the web page. It also includes the methods ad computed properties to support the implementation and performance of the app.
- **CSS (`style.css`):** Styles to define the appearance of the web page.
- **Component (`themeSwitcher.vue`):** This is the component for switching the theme of the app. It has all the functions supoorting for theme switch.
- **Fonts (`Poppins`):** Imported from Google Fonts for consistent typography.

## 5. Dependencies

- **Tailwind CSS:** Used for styling the components. It's linked through CDN in the `index.html` file.
- **Daisy UI:** A CSS library for UI components, linked through CDN.
- **Boxicons:** Icons library, linked through CDN.
- **Google Fonts (Poppins):** Font used for the app, linked in the `style.css` file.

## 6. Deployment

The TodoZen App is deployed and accessible online. You can use the following link to access the application: [TodoZen](Link)

## 7. Usage

1. **Adding a Task:**
   - Enter the task in the input field.
   - Optionally, set a due date using the date input.
   - Press Enter or click the "+" button to add the task.

2. **Editing a Task:**
   - Click the "Edit" button on a task.
   - Modify the task details.
   - Click the "Check" button to save changes.

3. **Completing a Task:**
   - Click the "Check" button on a task to toggle its completion status.

4. **Deleting a Task:**
   - Click the "Trash" button on a task to delete it.

5. **Filtering Tasks:**
   - Use the "Filter" dropdown to filter tasks by status (All, Pending, Completed).

6. **Clearing All Tasks:**
   - Click the "Delete All" button to clear all tasks.

7. **Theme Switching:**
   - Use the palette icon in the top-right corner to open the theme switcher.
   - Select a theme from the available options.
