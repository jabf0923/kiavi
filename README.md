# Spina CMS Local Developer Experience

## Project Overview
A Dockerized Ruby on Rails application with Spina CMS, designed for easy local development and testing.

## Prerequisites
- Docker(we will be using docker compose commands ) refer to this docs if needed https://docs.docker.com/reference/cli/docker/compose/#subcommands

## Setup and Running the Application

### Initial Setup
Clone the repository:
git clone [git@github.com:jabf0923/kiavi-lab.git]
cd kiavi

Add Spina gem version to test to your Gemfile:
e.g. "gem 'spina', '~> 2.18'"

Build and start the application:
`docker compose build` # this command will basically build the image or if needed pull down
`docker compose up -d` # this command will run the containers and create the network for both containers to communicate.

Create the database:
`docker compose exec web rails db:create` 

Install Active Storage:
`docker compose exec web rails active_storage:install` 

Initialize Spina:
`docker compose exec web rails spina:install`

### First-time Admin Setup
1. Navigate to http://localhost:3000/admin
2. Create initial admin account
   - Default credentials will be shown during Spina installation

## Detailed Feature Walkthrough

### a. Modifying the Home Page
1. Login to admin panel at http://localhost:3000/admin
2. Navigate to "Pages" section
3. Edit the home page
   - Modify text, layout, and content
   - Save changes

### b. Creating a New Page
1. In admin panel, go to "Pages"
2. Click "New Page"
3. Fill in:
   - Page title
   - Permalink
   - Choose a template
4. Add content and save

### c. Adding Text and Images
1. While editing a page:
   - Use rich text editor for text
   - Upload images via media library
   - Drag and drop content blocks
   - Customize page layout

### Persistent State Management
Data is persisted through Docker volumes. You can stop and restart containers without losing Spina configuration:

Stop containers:
`docker compose down`

Restart containers:
`docker compose up -d`

## Troubleshooting
- Ensure all containers are running: `docker compose ps`
- View logs: `docker compose logs web`
- Reset to clean state: `docker compose down -v` (caution: loses all data)

## Known Limitations
- Development environment only
- No production-grade security
- Simplified PostgreSQL configuration

## Updating Dependencies

To update gems:
1. Modify the Gemfile with desired gem versions.
2. Run:
`docker compose run web bundle update`

3. Rebuild the Docker image if needed:
`docker compose build`
