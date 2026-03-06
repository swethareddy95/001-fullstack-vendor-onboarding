# 01-fullstack-vendor-onboarding
# Trusted Vendors Portal – Full-Stack Assignment

## Objective
Welcome to your application assessment assignment. This is a chance for you to show us your coding and problem solving skills.
You are applying for a fullstack position so this assignment requires you to solve both frontend and backend challenges.

Nobody expects anyone to know everything so if a particular assignment is outside of your realm of experience, 
you may either skip it or propose a solution aligned with your experience.. 

In this repository, you'll find a basic demo implementation of the **Trusted Vendor Portal** application. 
Your task is to enhance and deploy this application by completing specific requirements listed below.

The system currently allows users to:
- Register a vendor (name, contact person, email, partner type [Supplier/Partner])
- View a list of registered vendors

---
## Vendor Object Example
    {
      "id": "1",
      "name": "Acme Freight",
      "contact_person": "John Doe",
      "email": "john.doe@acme.com",
      "partner_type": "Supplier" 
    }

## Existing Implementation

The repository contains:
- A Vue.js frontend application
- Two backend implementations (choose one):
  - Java (Spring Boot)
  - Node.js (TypeScript)

## Available Backends
You may choose which backend implementation to work with:

### Java (Spring Boot)
- Located in the `backend-java` directory
- Uses H2 in-memory database
- Includes basic create and list operations

### Node.js (TypeScript)
- Located in the `backend-node` directory 
- Uses SQLite database
- Includes basic create and list operations
---
## Your Tasks
### 1. Frontend UI Polish
- Refresh the `frontend` layout to highlight your CSS skills. Arrange the form and vendor list in a responsive layout that presents as a single column on mobile and a tidy multi-column layout on desktop using modern CSS (flexbox and/or grid).
- Introduce a lightweight design system by defining CSS variables (colours, spacing, typography) in `src/style.css` and apply them across components.
- Enhance the vendor list with hover/focus states, zebra striping, and an accessible empty state.
- Add a small visual flourish such as a light/dark theme toggle (or similar motif) handled with CSS-first techniques.
- Document the layout approach, design tokens, breakpoints, and accessibility considerations in this README

### 2. Delete vendor
- Implement a delete functionality to allow users to remove vendor entries from the system
- Include a confirmation dialog before deletion to prevent accidental removal.
- Update both frontend and your chosen backend to support this feature

### 3. Fix the UI bug
- Currently, clicking the "Add" button multiple times before the form resets can result in duplicate vendor entries.
- Prevent this behavior to improve the form UX

### 4. Unique Emails
- Ensure that vendor emails are unique across the system. If a user tries to register a vendor with a duplicate email, they should be informed of the conflict. 
  Think about where this logic should live and how the constraint is best enforced (frontend, backend, data storage or all) and justify your approach
- Document your reasoning

### 5. Containerization & Deployment (Optional)
At maerks we host most of our backend services using pods and k8. If you have experience or find the challenge interesting, give this assignment a go.

Choose one of the following deployment approaches:

#### Option A: Docker Compose
- Containerize your chosen backend using Docker
- Create a Docker Compose configuration to run the entire system (frontend + backend)
- Include clear instructions to build and start the application

#### Option B (Advanced): Kubernetes/Minikube Deployment
- Create Kubernetes manifests (YAML files) for both frontend and your chosen backend
- Ensure services can discover and communicate (e.g., using `ClusterIP`)
- Use **Minikube** to test locally
- Provide clear documentation or scripts to:
  - Build and push Docker images to Minikube's Docker daemon
  - Apply Kubernetes configs to start the app

You're welcome to make UX improvements or add minor enhancements, as long as the core requirements are clearly addressed.

---

## Evaluation Criteria
- **Code clarity & organisation** – Is the code readable, modular, testable and well-structured?
- **Testing** - How did you use testing to support your development efforts
- **Full-stack ownership** – Can you deliver a cohesive, working system with the required enhancements?
- **Pragmatism** – Did you make thoughtful decisions and sensible trade-offs?
- **DevOps awareness** – Is the system easy to build, run, and maintain?
- **Deployment quality** – If completed, is your containerization strategy practical, reproducible, and well-documented?"

---

## Submission Instructions

1. **Copy** this repository into your own GitHub account - do not fork or create a branch in this repository
2. Create a branch and complete the assigning in that branch.
4. **Documentation**
    1. Ensure your repository includes setup instructions and an updated README.md.
    2. Provide a short description of your approach to solving each task
    3. Highlight any assumptions, trade-offs, or challenges encountered during development.
5. In your readme.md file, also answer the following questions:
    1. What do I love most about being a software engineer.
    2. What is most important to me when it comes to working in a team
    3. What is the worst part of being a software engineer.
5. Create a pull request to the main branch and share the link to the pull request with us.
---

We're excited to see how you approach these tasks — feel free to get creative, make reasonable trade-offs, and show us how you think as an engineer. We're particularly interested in your understanding of full-stack development and DevOps practices.



---

# My Implementation & Approach

This section describes the changes and improvements I made while working on the assignment.

---

## 1. Frontend UI Polish

The frontend layout was redesigned to make the interface cleaner, more responsive, and easier to use.

### Responsive Layout

The layout uses **Flexbox** to ensure the application works well across different screen sizes.

- On **mobile screens**, the form and vendor list appear in a single column.
- On **larger screens**, the layout switches to a two-column structure where the form and vendor list appear side by side.

This approach keeps the UI simple and readable across devices.

---

### Lightweight Design System

A small design system was introduced using **CSS variables** in `src/style.css`.

These variables define reusable values such as:

- Colors
- Spacing
- Typography
- Border radius
- Shadows

Example variables:
--color-primary
--color-background
--space-md
--radius-md
--shadow-sm


Using design tokens makes the styling more consistent and easier to maintain.

---

### Vendor List Enhancements

The vendor list table was improved with several usability enhancements:

- **Zebra striping** to improve readability
- **Hover states** for rows
- **Focus styles** for accessibility
- **Responsive scrolling** for smaller screens
- An **empty state message** when no vendors are available

Example empty state:
No vendors found. Add your first vendor!

---

### Light / Dark Theme Toggle

A small visual enhancement was added by implementing a **light/dark theme toggle**.

The theme works by applying a `data-theme` attribute on the root element and switching CSS variables accordingly.

This allows the UI to switch themes without introducing additional libraries.

---

## 2. Fixing the Duplicate Submission Bug

In the original implementation, it was possible to click the **Add Vendor** button multiple times before the form reset, which could result in duplicate entries.

To prevent this, a submission lock was added to the form logic.

When the form is submitted:

- The submit button becomes disabled
- Additional clicks are ignored while the request is processing
- The form resets after submission

This improves the form UX and prevents accidental duplicate submissions.

---

## 3. Unique Vendor Emails

Vendor emails should ideally be unique across the system so that the same vendor cannot be registered multiple times.

Since the focus of my work was primarily on the **frontend improvements**, I did not modify the backend implementation in this repository.

However, while working on the solution I considered how this should ideally be implemented in a real system.

### Recommended Approach

In a production system, uniqueness should be enforced across multiple layers.

**Database Layer**

The email column should have a **UNIQUE constraint** to guarantee that duplicate email addresses cannot be stored.

**Backend Layer**

Before inserting a new vendor, the backend should check whether a vendor with the same email already exists and return an appropriate error response if a conflict is detected.

**Frontend Layer**

The frontend should display the error message returned by the API so the user understands why the vendor could not be added.

### Reasoning

Frontend validation alone cannot guarantee uniqueness because API requests can bypass the UI.  
For this reason, enforcing the constraint in the **database and backend layers** is the most reliable approach, while the frontend focuses on providing clear feedback to the user.

---

## Assumptions and Trade-offs

Since the primary focus of this assignment was the frontend, I focused on improving the UI, responsiveness, and user experience while keeping the implementation simple.

Backend functionality was left mostly unchanged except where required to understand how the frontend interacts with the API.

---

## Running the Project

### Start Backend
cd backend-node
npm install
npm run dev

Backend runs on: http://localhost:3000


### Start Frontend
cd frontend
npm install
npm run dev


Frontend runs on: http://localhost:5173


---

## Reflection

### What I love most about being a software engineer

What I enjoy most about software engineering is the ability to build solutions that solve real problems. I find it rewarding to take an idea and gradually turn it into a working system through design, coding, testing, and iteration.

### What is most important to me when working in a team

Clear communication and trust are the most important aspects of working in a team. When team members openly share ideas, feedback, and challenges, it becomes much easier to solve problems collaboratively and deliver better results.

### What is the worst part of being a software engineer

One of the more challenging aspects of software engineering is dealing with unclear requirements or constantly changing specifications. It can sometimes slow down development, but it also highlights the importance of communication and adaptability.


