# DevOps Project Report: CI/CD Pipeline and Microservices Development

## Team Members
1. **Amballa Venkata Sriram** (21bcs008)
2. **Devesh Kumar** (21bcs032)
3. **Mourya Kakarapu** (21bcs049)
4. **Karan Naik** (21bcs051)
5. **Abhishikt Mahajan** (21bcs060)
6. **Sujith Makam** (21bcs061)
7. **Aayushi Sinha** (21bcs120)
8. **Vishal Kumar** (21bcs133)
9. **Geeta Mahatme** (21bec024)
10. **Nupur Sangwai** (21bds046)

---

## Architecture

![Architecture Diagram](https://github.com/aelassas/microservices/blob/main/img/architecture.jpg?raw=true)

The application is built using a microservices architecture with the following services:

### Microservices
1. **Catalog Microservice**: Manages the catalog of items.
2. **Cart Microservice**: Manages the shopping cart.
3. **Identity Microservice**: Manages authentication and user information.

Each microservice has its own dedicated database, following the **database-per-service** pattern. This ensures better separation of concerns, scalability, and data isolation. Key advantages include:

- Independent schema updates.
- Prevents unauthorized cross-service data access.
- Independent scaling of services.
- Ability to use different database technologies per service.

### API Gateways
- **Frontend API Gateway**: Handles client-side requests.
- **Backend API Gateway**: Handles admin-side requests.

#### Frontend API Gateway Endpoints
- `GET /catalog`: Retrieves catalog items.
- `GET /catalog/{id}`: Retrieves a specific catalog item.
- `GET /cart`: Retrieves cart items.
- `POST /cart`: Adds an item to the cart.
- `PUT /cart`: Updates a cart item.
- `DELETE /cart`: Deletes a cart item.
- `POST /identity/login`: Logs in a user.
- `POST /identity/register`: Registers a new user.
- `GET /identity/validate`: Validates a JWT token.

#### Backend API Gateway Endpoints
- `GET /catalog`: Retrieves catalog items.
- `GET /catalog/{id}`: Retrieves a specific catalog item.
- `POST /catalog`: Creates a catalog item.
- `PUT /catalog`: Updates a catalog item.
- `DELETE /catalog/{id}`: Deletes a catalog item.
- `PUT /cart/update-catalog-item`: Updates catalog items in carts.
- `DELETE /cart/delete-catalog-item`: Deletes catalog item references from carts.
- `POST /identity/login`: Logs in a user.
- `GET /identity/validate`: Validates a JWT token.

---

### Screenshots

<img width="1222" alt="Screenshot 2024-11-14 at 8 28 44 PM" src="https://github.com/user-attachments/assets/95c39666-d7fb-4d15-9864-537f8528e10a">
<img width="1222" alt="Screenshot 2024-11-14 at 8 28 51 PM" src="https://github.com/user-attachments/assets/fe8835ef-8fd7-4132-a8f2-3d94f1b7342e">
<img width="1222" alt="Screenshot 2024-11-14 at 8 28 58 PM" src="https://github.com/user-attachments/assets/97038dad-380d-47d2-9009-6976f7bcf627">
<img width="1222" alt="Screenshot 2024-11-14 at 8 29 01 PM" src="https://github.com/user-attachments/assets/590bd501-0167-4699-ae9a-97dd8e9963c5">
<img width="1222" alt="Screenshot 2024-11-14 at 8 29 05 PM" src="https://github.com/user-attachments/assets/5998ca08-87fe-47df-8567-e62e33feed4d">
<img width="1222" alt="Screenshot 2024-11-14 at 8 29 08 PM" src="https://github.com/user-attachments/assets/ad42e439-2d48-447b-a4db-8bb30c8db2f4">
<img width="1222" alt="Screenshot 2024-11-14 at 8 29 11 PM" src="https://github.com/user-attachments/assets/efcec0f5-4b03-4ab0-9a1c-adfb9c272c09">









---

## Source Code

![Source Code](https://github.com/aelassas/microservices/blob/main/img/store-solution2.png?raw=true)

### Key Projects
- **CatalogMicroservice**: Source code for managing the catalog.
- **CartMicroservice**: Source code for managing the shopping cart.
- **IdentityMicroservice**: Source code for authentication and user management.
- **Middleware**: Common functionalities shared across microservices.
- **FrontendGateway**: Frontend API gateway.
- **BackendGateway**: Backend API gateway.
- **Frontend**: Client-side application.
- **Backend**: Admin-side application.
- **Tests**: Unit tests for all services.

Technologies used:
- Microservices: ASP.NET Core, C#
- Client Apps: HTML, Vanilla JavaScript

---

## How to Run the Application

1. **Open the Solution**: Load `store.sln` in Visual Studio 2022 as administrator.
2. **Setup MongoDB**: Ensure MongoDB is installed and running.
3. **Set Multiple Startup Projects**:
   - Right-click the solution in Visual Studio.
   - Select **Properties** > **Startup Projects**.
   - Enable all projects except `Middleware` and test projects.
4. **Run the Solution**:
   - Press **F5** to start the application.

### Access the Applications
- **Frontend**: [http://localhost:44317/](http://localhost:44317/)
- **Backend**: [http://localhost:44301/](http://localhost:44301/)


### Endpoints Overview
- **Frontend**: [http://localhost:44317/](http://localhost:44317/)
- **Backend**: [http://localhost:44301/](http://localhost:44301/)
- **Frontend Gateway**: [http://localhost:44300/](http://localhost:44300/)
- **Backend Gateway**: [http://localhost:44359/](http://localhost:44359/)
- **Identity Microservice**: [http://localhost:44397/](http://localhost:44397/)
- **Catalog Microservice**: [http://localhost:44326/](http://localhost:44326/)
- **Cart Microservice**: [http://localhost:44388/](http://localhost:44388/)

---
