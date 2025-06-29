
#  Airbnb Clone – Use Case Diagram

This repository contains the **Use Case Diagram** for the Airbnb Clone project. The diagram provides a high-level visual overview of how users (Guests, Hosts, and Admins) interact with the system across key functionalities such as **account management**, **property booking**, **payments**, and **notifications**.

---

##  Diagram Overview

The use case diagram includes the following actors and interactions:

###  Actors
- **Guest**: Can register, log in, book properties, make payments, and receive booking notifications.
- **Host**: Can register, list properties, manage bookings, receive payments, and get notified.
- **Admin**: Can log in and manage bookings, including cancellations and refunds.

###  Key Use Cases
- Register Account
- Log In (with extensions like Invalid Password)
- Book Property (with conditions like Booking Unavailable)
- Cancel Booking (which may trigger Refund Payment)
- Make Payment (with possible extension: Insufficient Balance)
- Receive and Process Payments
- Notifications to Host and Guest

---

##  Files
- `use_case_diagram_airbnb.drawio.png`: UML use case diagram image
- `README.md`: Project overview (this file)

---

##  Purpose

This diagram helps to:
- Visualize system functionality
- Clarify user interactions
- Serve as a guide for backend implementation

>  _Designed to ensure all key interactions are accounted for in system planning and feature development._

---

##  Related Resources

Check out the [Functionality Diagram]() and [ER Diagram]() for additional context.

---

##  Tools Used

- [draw.io](https://draw.io) for diagram creation
- Markdown for documentation

---

##  Feedback

Feel free to open an issue or submit suggestions for improving the clarity or completeness of the diagram.

---

> _“Clear diagrams make clean systems.”_ 💡
