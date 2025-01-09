# React EmailJS Contact Form with Vite

This repository demonstrates how to build a modern **React.js** contact form using **Vite** and **EmailJS**. The contact form includes:
- Form validation (name, email, message).
- Email sending through **EmailJS**.
- Integration with environment variables for secure credentials.

---

### **Table of Contents**

1. [What is EmailJS?](#what-is-emailjs)
2. [Why Vite?](#why-vite)
3. [Features of the Contact Form](#features-of-the-contact-form)
4. [Project Setup](#project-setup)
5. [How to Integrate EmailJS in Vite](#how-to-integrate-emailjs-in-vite)
6. [Full Code Implementation](#full-code-implementation)
7. [Customizing the Form](#customizing-the-form)
8. [Command Summary](#command-summary)

---

### **What is EmailJS?**

**EmailJS** allows sending emails directly from your frontend using their API, without requiring a backend. It integrates well with frameworks like React and works with services like Gmail, Outlook, and custom SMTP.

---

### **Why Vite?**

Vite offers:
- **Faster Builds**: Lightning-fast development server.
- **Modern Features**: Support for ESModules and JSX out of the box.
- **Environment Variable Support**: Makes handling API keys secure and seamless.

---

### **Features of the Contact Form**

- **Validation**: Prevents invalid form submissions.
- **Dynamic Error Messages**: Alerts users about missing or incorrect data.
- **EmailJS Integration**: Sends form data to your email using EmailJS.
- **Styling**: Includes basic CSS for a responsive layout.

---

### **Project Setup**

#### **1. Create a Vite React App**
Run the following command to create a new React project using Vite:

```bash
npm create vite@latest react-emailjs-contact-form --template react
```

Navigate to your project folder:

```bash
cd react-emailjs-contact-form
```

Install dependencies:

```bash
npm install
```

#### **2. Install EmailJS**
Install the `@emailjs/browser` library:

```bash
npm install @emailjs/browser
```

#### **3. Create a Free EmailJS Account**
- Sign up at [EmailJS](https://www.emailjs.com/).
- Create an **Email Service** and an **Email Template**.
- Copy your **Service ID**, **Template ID**, and **Public Key**.

#### **4. Set Up Environment Variables**
In the root directory of your project, create a `.env` file and add the following:

```env
VITE_EMAILJS_SERVICE_ID=your_service_id
VITE_EMAILJS_TEMPLATE_ID=your_template_id
VITE_EMAILJS_PUBLIC_KEY=your_public_key
```

> Replace `your_service_id`, `your_template_id`, and `your_public_key` with the actual values from your EmailJS account.

---

### **How to Integrate EmailJS in Vite**

Here’s how to integrate EmailJS into your Vite React project:

#### **1. Import Required Libraries**
Use the `useRef` hook from React and import `emailjs`.

```javascript
import React, { useRef } from 'react';
import emailjs from '@emailjs/browser';
```

#### **2. Create a Form Reference**
Set up a `ref` for the form to collect form data.

```javascript
const form = useRef();
```

#### **3. Define the `sendEmail` Function**
The function sends form data to EmailJS using the credentials from environment variables.

```javascript
const sendEmail = (e) => {
    e.preventDefault();

    emailjs.sendForm(
        import.meta.env.VITE_EMAILJS_SERVICE_ID,
        import.meta.env.VITE_EMAILJS_TEMPLATE_ID,
        form.current,
        import.meta.env.VITE_EMAILJS_PUBLIC_KEY
    )
    .then(() => {
        alert('Message sent successfully!');
        form.current.reset();
    })
    .catch(() => {
        alert('Failed to send the message. Please try again.');
    });
};
```

---

### **Full Code Implementation**

Here’s the complete code for the contact form:

#### **Contact.jsx**
```javascript
import React, { useRef } from 'react';
import emailjs from '@emailjs/browser';

const Contact = () => {
    const form = useRef();

    const sendEmail = (e) => {
        e.preventDefault();

        emailjs.sendForm(
            import.meta.env.VITE_EMAILJS_SERVICE_ID,
            import.meta.env.VITE_EMAILJS_TEMPLATE_ID,
            form.current,
            import.meta.env.VITE_EMAILJS_PUBLIC_KEY
        )
        .then(() => {
            alert('Message sent successfully!');
            form.current.reset();
        })
        .catch(() => {
            alert('Failed to send the message. Please try again.');
        });
    };

    return (
        <div className="contact-section">
            <div className="container">
                <h2>Contact Me</h2>
                <form ref={form} onSubmit={sendEmail}>
                    <div className="custom-input">
                        <input type="text" name="from_name" placeholder="Your Name" required />
                    </div>
                    <div className="custom-input">
                        <input type="email" name="from_email" placeholder="Your Email" required />
                    </div>
                    <div className="custom-input textarea">
                        <textarea name="message" placeholder="Your Message" required></textarea>
                    </div>
                    <button type="submit" className="btn">Send Message</button>
                </form>
            </div>
        </div>
    );
};

export default Contact;
```

---

### **Customizing the Form**

- **Styling**: Modify the CSS file (`Contact.css`) to match your design preferences.
- **Validation**: Add custom validation logic to meet your requirements.
- **Email Templates**: Adjust the EmailJS email template to personalize email content.

---

### **Command Summary**

| Command                  | Description                               |
|--------------------------|-------------------------------------------|
| `npm install`            | Install project dependencies             |
| `npm run dev`            | Start the development server             |
| `npm run build`          | Build the project for production         |
| `git clone <repo-url>`   | Clone this GitHub repository             |

---

### **Conclusion**

Using this guide, you can create a functional and beautiful contact form in React with Vite and EmailJS. It’s lightweight, fast, and perfect for modern web projects.

Feel free to contribute to this repository and enhance its features! 🚀
