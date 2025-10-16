# Travel Management System - CI/CD Deployment

This repository contains a full-stack Travel Management System with Spring Boot backend and React frontend, configured for containerized deployment using Docker Compose.

## System Architecture

- **Frontend**: React + Vite (runs on localhost:5173)
- **Backend**: Spring Boot + MySQL (runs on localhost:8081) 
- **Database**: MySQL 8.0
- **Containerization**: Docker & Docker Compose

## Prerequisites

- Docker and Docker Compose installed
- Git
- Ports 5173, 8081, and 3306 available on your system

## Quick Start

### 1. Clone and Setup
```bash
# Navigate to project directory
cd /home/vishnu/Downloads/cicd

# Verify all components are present
ls -la
# Should see: travel-frontend/, travel-backend/, docker-compose.yaml
```

### 2. Deploy with Docker Compose
```bash
# Build and start all services
docker-compose up --build

# Or run in detached mode
docker-compose up --build -d
```

### 3. Access the Application
- **Frontend**: http://localhost:5173
- **Backend API**: http://localhost:8081
- **Database**: localhost:3306

### 4. Test the System
1. Open browser to http://localhost:5173
2. Test signup functionality to create a new user
3. Test login functionality with created credentials
4. Verify backend API responses at http://localhost:8081

## Service Details

### Travel Frontend Service
- **Container**: travel-frontend
- **Port Mapping**: 5173:3000
- **Technology**: React + Vite
- **Environment**: Points to backend at http://localhost:8081

### Travel Backend Service
- **Container**: travel-backend
- **Port Mapping**: 8081:8081
- **Technology**: Spring Boot + JPA
- **Database**: MySQL connection with auto-schema creation

### MySQL Database Service
- **Container**: travel-mysql
- **Port Mapping**: 3306:3306
- **Database**: travelmanagement
- **Credentials**: root/root123, travel/travel123

## Development Commands

```bash
# View running containers
docker-compose ps

# View logs
docker-compose logs
docker-compose logs travel-frontend
docker-compose logs travel-backend
docker-compose logs travel-mysql

# Stop services
docker-compose down

# Rebuild specific service
docker-compose build travel-backend
docker-compose up travel-backend

# Clean restart (removes volumes)
docker-compose down -v
docker-compose up --build
```

## API Endpoints

The backend exposes REST APIs for:
- User authentication (signup/login)
- Travel bookings management
- Payment processing
- User profile management

Base URL: http://localhost:8081

## Troubleshooting

### Common Issues

1. **Port Conflicts**
   ```bash
   # Check if ports are in use
   sudo netstat -tulpn | grep :5173
   sudo netstat -tulpn | grep :8081
   sudo netstat -tulpn | grep :3306
   ```

2. **Database Connection Issues**
   ```bash
   # Check MySQL logs
   docker-compose logs travel-mysql
   
   # Connect to database directly
   docker exec -it travel-mysql mysql -u root -p
   ```

3. **Frontend Build Issues**
   ```bash
   # Rebuild frontend only
   docker-compose build travel-frontend
   docker-compose up travel-frontend
   ```

4. **Backend Build Issues**
   ```bash
   # Check Java version and Maven build
   docker-compose build travel-backend
   docker-compose logs travel-backend
   ```

### Clean Reset
```bash
# Complete cleanup and restart
docker-compose down -v
docker system prune -f
docker-compose up --build
```

## CI/CD Best Practices Implemented

1. **Containerization**: All services containerized with multi-stage builds
2. **Environment Configuration**: Environment-specific configurations
3. **Service Dependencies**: Proper service startup order with depends_on
4. **Health Checks**: Implicit health checking through service dependencies
5. **Volume Management**: Persistent data storage for MySQL
6. **Network Isolation**: Custom Docker network for service communication
7. **Port Management**: Clear port mapping strategy
8. **Build Optimization**: Docker layer caching and multi-stage builds

## Monitoring and Logs

Monitor the application health:
```bash
# Real-time logs from all services
docker-compose logs -f

# Check container health
docker-compose ps
docker stats
```

## Production Considerations

For production deployment:
1. Use environment-specific configuration files
2. Implement proper secrets management
3. Add health check endpoints
4. Configure reverse proxy (nginx)
5. Set up monitoring and alerting
6. Implement backup strategies for database
7. Use container orchestration (Kubernetes)

## Support

For issues and questions:
1. Check application logs
2. Verify all services are running
3. Ensure database connectivity
4. Confirm port availability
# cicd-lab
# cicd-lab1
# cicd-lab1
