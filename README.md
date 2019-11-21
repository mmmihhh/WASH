# WASH
SCCM Helper - add users/devices to collections

This project scope is to simplify the process of adding users and devices to SCCM Collections. Also, this software will allow users (like your support team) to deploy software without having SCCM rights.


There are few steps you need to do as a pre-requisite to make this project work.

Step 1:
Create a SQL database with 2 tables (I named them Operations and Collections). Here are the table structures:

CREATE TABLE [dbo].[Operations] (
    [Id]                 INT            IDENTITY (1, 1) NOT NULL,
    [OperationName]      NVARCHAR (MAX) NOT NULL,
    [CollectionName]     NVARCHAR (MAX) NOT NULL,
    [CollectionID]       NVARCHAR (MAX) NOT NULL,
    [ComputerResourceID] NVARCHAR (MAX) DEFAULT ('None') NOT NULL,
    [ComputerName]       NVARCHAR (MAX) DEFAULT ('None') NOT NULL,
    [UserResourceID]     NVARCHAR (MAX) DEFAULT ('None') NOT NULL,
    [UserSamID]          NVARCHAR (MAX) DEFAULT ('None') NOT NULL,
    [UserUPN]            NVARCHAR (MAX) DEFAULT ('None') NOT NULL,
    [UserEmail]          NVARCHAR (MAX) DEFAULT ('None') NOT NULL,
    [NotificationEmail]  NVARCHAR (MAX) NOT NULL,
    [DeploymentDate]     DATE           DEFAULT (getdate()) NOT NULL,
    [DeploymentTime]     TIME (0)       DEFAULT (getdate()) NOT NULL,
    [Executed]           NVARCHAR (MAX) DEFAULT ('No') NOT NULL,
    [SendEmailToUser]    NVARCHAR (MAX) DEFAULT ('No') NOT NULL,
    [EmailSentToUser]    NVARCHAR (MAX) DEFAULT ('No') NOT NULL,
    [Error]              NVARCHAR (MAX) DEFAULT ('None') NOT NULL,
    [EmailSent]          NVARCHAR (MAX) DEFAULT ('No') NOT NULL,
    [EmailSentError]     NVARCHAR (MAX) DEFAULT ('None') NOT NULL,
    [commitedBy]         NVARCHAR (50)  NULL,
    [commitedOn]         DATETIME2 (7)  NULL,
    [deletedBy]          NVARCHAR (50)  NULL,
    [deletedOn]          DATETIME2 (7)  NULL,
    [addedBy]            NVARCHAR (50)  DEFAULT ('Admin') NOT NULL,
    [addedOn]            DATETIME2 (7)  DEFAULT (getdate()) NOT NULL,
    PRIMARY KEY CLUSTERED ([Id] ASC)
);

CREATE TABLE [dbo].[Collections] (
    [Id]                     INT            IDENTITY (1, 1) NOT NULL,
    [CollectionName]         NVARCHAR (MAX) NOT NULL,
    [CollectionID]           NVARCHAR (MAX) NOT NULL,
    [CollectionFriendlyName] NVARCHAR (MAX) DEFAULT ('None') NOT NULL,
    [CollectionComment]      NVARCHAR (MAX) DEFAULT ('None') NOT NULL,
    [deletedBy]              NVARCHAR (50)  NULL,
    [deletedOn]              DATETIME2 (7)  NULL,
    [addedBy]                NVARCHAR (50)  DEFAULT ('Admin') NOT NULL,
    [addedOn]                DATETIME2 (7)  DEFAULT (getdate()) NOT NULL,
    PRIMARY KEY CLUSTERED ([Id] ASC)
);

Step 2:
Open this project file and rename all the needed variables to match your needs

Step 3:
Make sure the user using this app is part of the AD group you setup in the above step


