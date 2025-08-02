# Task Management Application

## Overview

This is a complete full-stack task management application built with Node.js, Express.js, and React. The application provides comprehensive task management capabilities including CRUD operations, image uploads with thumbnail generation, background job processing, and email notifications. It features a modern UI with real-time updates and a robust queue system for handling asynchronous operations.

**Status: Fully Operational** - The application is successfully deployed and running with all core features functional.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
The frontend is built with React 18 and uses modern development tools:
- **UI Framework**: React 18 with TypeScript for type safety
- **Styling**: Tailwind CSS with shadcn/ui components for consistent design
- **State Management**: TanStack Query (React Query) for server state management
- **Routing**: Wouter for client-side routing
- **Build Tool**: Vite for fast development and optimized builds
- **Real-time Communication**: WebSocket connection for live updates

### Backend Architecture
The backend follows a modular Express.js structure:
- **Framework**: Express.js 5 with TypeScript
- **Database Layer**: Drizzle ORM with PostgreSQL using Neon serverless
- **Queue System**: BullMQ with Redis for background job processing
- **File Handling**: Multer for file uploads with Sharp for image processing
- **Email Service**: Nodemailer for email notifications
- **Real-time Updates**: WebSocket server for broadcasting updates

### Database Design
PostgreSQL database with the following core tables:
- **tasks**: Main task entities with title, description, priority, status, and processing type
- **images**: File metadata linked to tasks with original and thumbnail URLs
- **email_logs**: Email tracking with status, retry count, and error logging
- **Status Enums**: Priority (low/medium/high), status (pending/processing/completed), email status (pending/sent/failed)

### Queue Processing Architecture
Three specialized worker queues handle different aspects of task processing:
- **taskProcessor**: Simulates task processing with configurable delays (fast/standard/slow)
- **imageUpload**: Generates 256px thumbnails using Sharp image processing
- **emailDispatch**: Handles email notifications with retry logic and error tracking

### File Storage Strategy
Local file storage system with organized structure:
- Original images stored in server/uploads directory
- Thumbnails generated and stored alongside originals
- Database stores file paths and metadata for efficient retrieval

## External Dependencies

### Database Services
- **Neon PostgreSQL**: Serverless PostgreSQL database with WebSocket support
- **Drizzle ORM**: Type-safe database operations with schema management

### Queue and Caching
- **Redis**: Message broker for BullMQ queue system
- **BullMQ**: Robust job queue with retry logic and progress tracking

### Email Services
- **Nodemailer**: Email sending with SMTP transport
- **Mailhog/Mailtrap**: Development email testing (configurable via environment)

### Image Processing
- **Sharp**: High-performance image resizing and thumbnail generation
- **Multer**: Multipart form data handling for file uploads

### UI and Styling
- **Radix UI**: Accessible component primitives
- **Tailwind CSS**: Utility-first CSS framework
- **Lucide React**: Icon library for consistent iconography

### Development Tools
- **TypeScript**: Type safety across frontend and backend
- **Zod**: Runtime type validation and schema definition
- **ESBuild**: Fast JavaScript bundling for production builds