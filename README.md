# 📖 Project Nexus - ProDev Backend Engineering

## 📌 Overview
Project Nexus is a **documentation hub** consolidating my major learnings from the **ProDev Backend Engineering program**.  
It highlights the backend technologies, concepts, challenges, and solutions I encountered, and serves as a **reference guide** for future learners.  

As a case study, I showcase my **Social Media Feed Backend** project — a scalable backend system that simulates real-world applications like Twitter or Instagram, with GraphQL APIs, CRUD operations, and user interactions.

---

## 🎯 Project Objective
- Consolidate **key learnings** from the ProDev Backend Engineering program.  
- Document **backend technologies, concepts, challenges, and solutions**.  
- Serve as a **knowledge hub** for backend learners.  
- Demonstrate collaboration between **frontend and backend developers**.  

---

## 🛠️ Key Technologies Covered
- **Python** (3.10+)  
- **Django** (backend framework)  
- **GraphQL** (Graphene-Django)  
- **PostgreSQL** (relational database)  
- **Docker & docker-compose** (containerization)  
- **Redis** (caching)  
- **Celery + RabbitMQ** (async tasks)  
- **CI/CD Pipelines** (GitHub Actions + deployment)  

---

## 📚 Important Backend Concepts
### 1. Database Design
- Normalization of data models.  
- Designing relationships for users, posts, comments, and likes.  
- Using indexes and constraints for performance.  

### 2. Asynchronous Programming
- Handling background tasks with **Celery + RabbitMQ**.  
- Examples: sending notifications, analytics jobs, scheduled tasks.  

### 3. Caching Strategies
- Using **Redis** for frequently accessed queries (e.g., feeds, trending posts).  
- Improving response times by avoiding repeated expensive queries.  

### 4. GraphQL-Only API
- No REST endpoints.  
- Users, posts, and interactions exposed through a schema.  

---
### 🚀 Getting Started

1. Clone the Repository
- git clone https://github.com/CiiruNgunjiri/alx-project-nexus.git
- cd alx-project-nexus

2. Create a Virtual Environment
- python -m venv .venv
- source .venv/bin/activate  # Linux/macOS
- .venv\Scripts\activate     # Windows

3. Install Dependencies
- pip install -r requirements.txt

4. Setup Environment Variables
- Create a .env file in the project root:
DJANGO_SECRET_KEY=your_secret_key
DJANGO_DEBUG=True
DJANGO_ALLOWED_HOSTS=127.0.0.1,localhost

POSTGRES_DB=database-name
POSTGRES_USER= username
POSTGRES_PASSWORD= password
POSTGRES_HOST_LOCAL=127.0.0.1
POSTGRES_PORT_LOCAL=5432

REDIS_URL=redis://localhost:6379/1
CELERY_BROKER_URL=amqp://guest:guest@localhost:5672//
CELERY_RESULT_BACKEND=redis://localhost:6379/2

CORS_ALLOWED_ORIGINS=http://localhost:3000
CSRF_TRUSTED_ORIGINS=http://localhost:3000
MEDIA_URL=/media/
MEDIA_ROOT=/path/to/media

# ⚠️ Update the values according to your local setup or Docker configuration.

5. Apply Migrations
- python manage.py makemigrations
- python manage.py migrate

6. Create a Superuser (Optional)
- python manage.py createsuperuser

7. Run the Development Server
- python manage.py runserver

- Open your browser: http://127.0.0.1:8000/

## Run with docker:
- docker-compose up --build
- docker-compose run --rm web python manage.py migrate
- docker-compose run --rm web python manage.py createsuperuser

# Access App
Backend API: http://127.0.0.1:8000/graphql/
Admin Panel: http://127.0.0.1:8000/admin/

### ⚡ Case Study: Social Media Feed Backend
## Real-World Application
A backend system for managing posts, user interactions, and personalized feeds.  
Key learnings included:  
- Using **GraphQL** for flexible data fetching.  
- Designing schemas for **high-traffic user interactions**.  
- Optimizing queries and using **caching** for performance.  

### Goals
- **Post Management (CRUD):** Create, read, update, and delete posts.  
- **User Management (CRUD):** Manage profiles, authentication, and ownership of posts.  
- **Follow System:** Users can follow/unfollow others.  
- **Feed:** Personalized feed of posts from followed users, sorted by newest first.  
- **Interactions:** Users can like, comment, and share posts.  

## Features
- User Authentication & Profiles
- Post Management (CRUD) with image URL field
- Follow System (users can follow/unfollow)
- Personalized Feeds sorted by newest posts
- Interactions: likes, comments

---

## 📊 System Design

### Entity-Relationship Diagram (ERD)
```mermaid
erDiagram
    USER ||--o{ POST : "creates"
    USER ||--o{ FOLLOW : "follows"
    USER ||--o{ COMMENT : "writes"
    USER ||--o{ LIKE : "likes"

    POST ||--o{ COMMENT : "has"
    POST ||--o{ LIKE : "receives"

    USER {
        int id PK
        string username
        string email
        string password
        string bio
        string profile_picture
    }

    POST {
        int id PK
        string content
        string media_url
        datetime created_at
    }

    FOLLOW {
        int id PK
        int follower_id FK
        int following_id FK
    }

    COMMENT {
        int id PK
        string text
        datetime created_at
    }

    LIKE {
        int id PK
        datetime created_at
    }
```

### Workflow
```mermaid
flowchart TD
    A[User Registers/Login] --> B[Create Post]
    B --> C[Feed Updates]
    A --> D[Follow User]
    D --> C
    A --> E[Like/Comment Post]
    E --> C
    C --> F[GraphQL Feed Query]
    F --> G[Return Personalized Feed]
```

💻 Example GraphQL Queries
# Create a User
mutation {
  createUser(username: "alice", email: "alice@mail.com", password: "12345") {
    user {
      id
      username
    }
  }
}
# Fetch Personalized Feed
{
  feed(userId: 1) {
    id
    content
    author {
      username
    }
    createdAt
  }
}

### 🔑 Challenges & Solutions
* Challenge: GraphQL file upload issues.
Solution: Rolled back to using image_url (string field) for reliability.

* Challenge: CORS errors in deployment.
Solution: Configured CORS_ALLOWED_ORIGINS and CSRF_TRUSTED_ORIGINS in settings.

* Challenge: Background processing.
Solution: Integrated Celery + RabbitMQ.

### 🏆 Best Practices & Takeaways

- Modular Django apps and GraphQL schema separation.
- CI/CD pipelines ensure automated builds + tests.
- Redis + Celery for scalability.
- Clear commit workflow (feat:, fix:, docs:).
- Collaboration with frontend developers ensured smooth API integration.

### 🤝 Collaboration

- Collaborated with ProDev Frontend learners who consumed the APIs.
- Shared ideas and solutions in the #ProDevProjectNexus Discord channel and other relevant channels of communication.
- Organized joint study sessions for debugging and API testing.

### 📅 Git Commit Workflow

- feat: → new features (e.g., posts CRUD, follow system).
- fix: → bug fixes.
- perf: → performance improvements (query optimization).
- docs: → README and documentation updates.

### 📊 Evaluation Criteria

- Functionality – APIs for posts, users, and interactions.

- Code Quality – clean, modular, well-structured code.

- User Experience – intuitive GraphQL Playground.

- Version Control – frequent commits with meaningful messages.

![Backend CI](https://github.com/CiiruNgunjiri/alx-project-nexus/actions/workflows/ci.yml/badge.svg?branch=feature/ci-setup)

### 👩‍💻 Author
Ciiru Ngunjiri
ProDev Backend Engineer

- GitHub: CiiruNgunjiri (https://github.com/CiiruNgunjiri)
- Linkedin: Linda Ngunjiri (www.linkedin.com/in/linda-ngunjiri35)
- Email: ciiru.ngunjiri@gmail.com
