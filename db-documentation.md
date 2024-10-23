# Housing Society Management System - Database Documentation


## Database Schema

### Core Tables

#### Societies
Primary table for housing societies.
- `society_id` (INT, PK): Unique identifier for each society
- `name` (VARCHAR(100)): Society name
- `address` (TEXT): Complete address of the society
- `created_at`, `updated_at`: Timestamps for record tracking

#### Users
Stores all user information across roles.
- `user_id` (INT, PK): Unique identifier for each user
- `username` (VARCHAR(50), UNIQUE): Unique username
- `email` (VARCHAR(100), UNIQUE): User's email address
- `password` (VARCHAR(255)): Hashed password
- `role` (ENUM): One of 'admin', 'manager', 'resident'
- `profile_info` (TEXT): Additional user information
- `created_at`, `updated_at`: Timestamps for record tracking

#### Flats
Represents individual residential units.
- `flat_id` (INT, PK): Unique identifier for each flat
- `society_id` (INT, FK): Reference to Societies table
- `flat_number` (VARCHAR(10)): Flat identification number
- `created_at`, `updated_at`: Timestamps for record tracking
**Unique Constraint**: Combination of `society_id` and `flat_number` must be unique

### Mapping Tables

#### UserFlats
Maps users to flats, handling ownership and tenancy.
- Primary Key: Combination of `user_id` and `flat_id`
- `is_owner` (BOOLEAN): Indicates if user owns the flat
- `start_date` (DATE): Start date of ownership/tenancy
- `end_date` (DATE): End date of tenancy (NULL for owners)
- Foreign Keys:
  - `user_id` references Users
  - `flat_id` references Flats

### Community Management

#### Complaints
Tracks resident complaints and their status.
- `complaint_id` (INT, PK): Unique identifier
- `user_id` (INT, FK): User who filed the complaint
- `society_id` (INT, FK): Related society
- `title` (VARCHAR(100)): Brief complaint title
- `description` (TEXT): Detailed complaint description
- `status` (ENUM): One of 'open', 'in_progress', 'resolved', 'closed'

#### Payments
Records all financial transactions.
- `payment_id` (INT, PK): Unique identifier
- `user_id`, `flat_id` (INT, FK): Related user and flat
- `amount` (DECIMAL(10,2)): Payment amount
- `payment_date` (DATE): Date of payment
- `status` (ENUM): One of 'pending', 'completed', 'failed', 'refunded'
- `description` (VARCHAR(255)): Payment description

#### Events
Manages society events and gatherings.
- `event_id` (INT, PK): Unique identifier
- `society_id` (INT, FK): Related society
- `title` (VARCHAR(100)): Event title
- `description` (TEXT): Event details
- `event_date` (DATETIME): Date and time of event
- `created_by` (INT, FK): User who created the event

#### Notices
Handles society announcements and notices.
- `notice_id` (INT, PK): Unique identifier
- `society_id` (INT, FK): Related society
- `title` (VARCHAR(100)): Notice title
- `content` (TEXT): Notice content
- `notice_date` (DATE): Publication date
- `created_by` (INT, FK): User who created the notice

### Community Engagement

#### Polls
Manages community polls and voting.
- `poll_id` (INT, PK): Unique identifier
- `society_id` (INT, FK): Related society
- `question` (TEXT): Poll question
- `start_date`, `end_date` (DATE): Poll duration
- `created_by` (INT, FK): Poll creator

#### PollOptions
Stores options for each poll.
- `option_id` (INT, PK): Unique identifier
- `poll_id` (INT, FK): Related poll
- `option_text` (VARCHAR(255)): Option text

#### PollVotes
Records user votes in polls.
- `vote_id` (INT, PK): Unique identifier
- `poll_id`, `user_id`, `option_id` (INT, FK): Related entities
**Unique Constraint**: Each user can only vote once per poll

### Emergency Information

#### EmergencyContacts
Stores emergency contact information.
- `contact_id` (INT, PK): Unique identifier
- `society_id` (INT, FK): Related society
- `name` (VARCHAR(100)): Contact person name
- `phone_number` (VARCHAR(15)): Contact number
- `role` (VARCHAR(50)): Role/designation

## Important Notes

### Timestamps
- All tables include `created_at` and `updated_at` fields
- Default value: `CURRENT_TIMESTAMP()`
- Useful for audit trails and record tracking

### Foreign Key Relationships
- All relationships are properly constrained with foreign keys
- Ensures data integrity across the system
- Consider implementing appropriate CASCADE rules based on business requirements

### Unique Constraints
1. Users table:
   - Unique username
   - Unique email
2. Flats table:
   - Unique combination of society_id and flat_number
3. PollVotes table:
   - One vote per user per poll

### Enums
1. User Roles: 'admin', 'manager', 'resident'
2. Complaint Status: 'open', 'in_progress', 'resolved', 'closed'
3. Payment Status: 'pending', 'completed', 'failed', 'refunded'

