**&larr; [Back to Program README](../README.md)**
# Project 2 - C# Microservice Reference Design & Implementation 

  - [Introduction](#introduction)
  - [Tasks](#tasks)
  - [Database Design](#database-design)

* [Development Environment & Setup](project2-c#/docs/development-environment.md)
* [API Design](project2-c#/docs/endpoints.md)
* [Application Archtecture](docs/architecture.md)
---

## Introduction

Project 2 is concerned with a C# ASP.NET MVC microservice in which you will need implement the <a href="docs/endpoints.md">REST API</a> as defined for Project 1.

![](../../docs/images/Projects-Boundary.png){width=500px}
<figcaption><b>Fig.1 - Project Boundaries </b></figcaption>

---
## Tasks

The following lists the tasks required for Project 1,2

>**Feature: Register Seller**  
**Feature: Manage Properties**  
**Feature: Register Buyer**  
**Feature: Manage Booking**
> 
> - For each feature create the controller, DTO, mapping and entity for each domain : 
>   - Seller <mark>*Minimum Requirement<mark/>
>   - Buyer <mark>*Minimum Requirement<mark/>
>   - Property <mark>*Minimum Requirement<mark/>
>   - Booking *<mark>This is needed if you have implemented Booking in the frontend<mark/>
> - Create e2e tests 


## Database Design

You'll need to design the database schema for Estate Agent Application.  We can identify four domains from the case study requirements:

- SELLER
- PROPERTY
- BUYER
- BOOKING

### Database Schema

Figure 2 below shows the database schema after normalization:

![](../../docs/images/Database-Schema.png){width=800px}
<figcaption><b>Fig.2 - Database Schema</b></figcaption>

### Database Script
```sql
USE [master]
GO

DROP DATABASE IF EXISTS [estateagent]
GO

CREATE DATABASE [estateagent]
GO

USE [estateagent]
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[booking](
	[BOOKING_ID] [int] IDENTITY(4,1) NOT NULL,
	[BUYER_ID] [int] NOT NULL,
	[PROPERTY_ID] [int] NOT NULL,
	[TIME] [datetime] NULL,
 CONSTRAINT [PK_booking_BOOKING_ID] PRIMARY KEY CLUSTERED 
(
	[BOOKING_ID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[buyer](
	[BUYER_ID] [int] IDENTITY(4,1) NOT NULL,
	[FIRST_NAME] [nvarchar](255) NOT NULL,
	[SURNAME] [nvarchar](255) NOT NULL,
	[ADDRESS] [nvarchar](255) NOT NULL,
	[POSTCODE] [nvarchar](255) NOT NULL,
	[PHONE] [nvarchar](20) NOT NULL,
 CONSTRAINT [PK_buyer_BUYER_ID] PRIMARY KEY CLUSTERED 
(
	[BUYER_ID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[property](
	[PROPERTY_ID] [int] IDENTITY(5,1) NOT NULL,
	[ADDRESS] [nvarchar](255) NOT NULL,
	[POSTCODE] [nvarchar](255) NOT NULL,
	[TYPE] [nvarchar](9) NOT NULL,
	[NUMBER_OF_BEDROOMS] [int] NOT NULL,
	[NUMBER_OF_BATHROOMS] [int] NOT NULL,
	[GARDEN] [binary](1) NOT NULL,
	[PRICE] [decimal](11, 2) NULL,
	[STATUS] [nvarchar](9) NOT NULL,
	[SELLER_ID] [int] NOT NULL,
	[BUYER_ID] [int] NULL,
 CONSTRAINT [PK_property_PROPERTY_ID] PRIMARY KEY CLUSTERED 
(
	[PROPERTY_ID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[seller](
	[SELLER_ID] [int] IDENTITY(11,1) NOT NULL,
	[FIRST_NAME] [nvarchar](255) NOT NULL,
	[SURNAME] [nvarchar](255) NOT NULL,
	[ADDRESS] [nvarchar](255) NOT NULL,
	[POSTCODE] [nvarchar](255) NOT NULL,
	[PHONE] [nvarchar](20) NOT NULL,
 CONSTRAINT [PK_seller_SELLER_ID] PRIMARY KEY CLUSTERED 
(
	[SELLER_ID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[booking] ADD  DEFAULT (NULL) FOR [TIME]
GO
ALTER TABLE [dbo].[property] ADD  DEFAULT (NULL) FOR [PRICE]
GO
ALTER TABLE [dbo].[property] ADD  DEFAULT (NULL) FOR [BUYER_ID]
GO
ALTER TABLE [dbo].[booking]  WITH NOCHECK ADD  CONSTRAINT [booking$booking_ibfk_1] FOREIGN KEY([BUYER_ID])
REFERENCES [dbo].[buyer] ([BUYER_ID])
GO
ALTER TABLE [dbo].[booking] CHECK CONSTRAINT [booking$booking_ibfk_1]
GO
ALTER TABLE [dbo].[booking]  WITH NOCHECK ADD  CONSTRAINT [booking$booking_ibfk_2] FOREIGN KEY([PROPERTY_ID])
REFERENCES [dbo].[property] ([PROPERTY_ID])
GO
ALTER TABLE [dbo].[booking] CHECK CONSTRAINT [booking$booking_ibfk_2]
GO
ALTER TABLE [dbo].[property]  WITH NOCHECK ADD  CONSTRAINT [property$property_ibfk_1] FOREIGN KEY([SELLER_ID])
REFERENCES [dbo].[seller] ([SELLER_ID])
GO
ALTER TABLE [dbo].[property] CHECK CONSTRAINT [property$property_ibfk_1]
GO
ALTER TABLE [dbo].[property]  WITH NOCHECK ADD  CONSTRAINT [property$property_ibfk_2] FOREIGN KEY([BUYER_ID])
REFERENCES [dbo].[buyer] ([BUYER_ID])
GO
ALTER TABLE [dbo].[property] CHECK CONSTRAINT [property$property_ibfk_2]
GO
```
