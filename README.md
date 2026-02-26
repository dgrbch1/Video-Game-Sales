🎮 Video Game Sales Data Warehouse
A full end-to-end Business Intelligence project that builds a data warehouse from a real-world video game sales dataset, performs ETL processing, constructs an OLAP cube, and delivers business insights through Excel PivotTable reports.

📋 Project Overview
DetailInfoDatasetVideo Game Sales (sourced from Data.world)GoalBuild a data warehouse and analyze global video game sales by platform, genre, region, and publisherTeamSyed Asghar, Tonny Li, Christopher GSchoolNew York City College of Technology

🛠️ Tools & Technologies

SQL Server / SSMS – Database storage and management
Visual Studio – SSIS (ETL) and SSAS (OLAP Cube) development
SSIS (ETL) – Data extraction, transformation, and loading
SSAS – Multidimensional cube creation and analysis
ERD+ – Entity Relationship Diagram design
Excel – Data cleansing and PivotTable reporting


🗄️ Database Architecture
Star Schema Design
The warehouse follows a star schema with the following tables:
Staging Table (StageVideoGame)

Holds cleaned raw data before loading into dimensions and fact table
Fields: StageKey, SourceID, VideoGameKey, RankKey, Name, Platform, Year, Genre, Publisher, NA_Sales, EU_Sales, JP_Sales, Other_Sales, Global_Sales

Dimension Tables

DimVideoGame – VideoGameKey (PK), SourceID, Name, Platform, Year, Genre, Publisher
DimRank – RankKey (PK), SourceID, Rank

Fact Table

FactSales – FactSalesKey (PK), VideoGameKey (FK), RankKey (FK), NA_Sales, EU_Sales, JP_Sales, Other_Sales, Global_Sales


⚙️ ETL Process (SSIS)

Raw data imported and cleansed in Excel (removed bugged/error rows)
SSIS data flow loads cleaned data into the staging table
Dimension tables populated from staging table via SSIS data flows
Dimension keys updated on the staging table
Fact table populated from staging table
Primary keys and foreign key constraints applied to enforce relationships


📊 SSAS Cube

Cube Name: Video Games Cube
Measure Group: FactSales
Measures: NA Sales, EU Sales, JP Sales, Other Sales, Global Sales
Dimensions: Dim Video Game, Dim Rank
Connected via Windows Authentication to SQL Server


📈 Key Findings
Platform Sales

PS2 was the top-selling platform globally with $1,255M in total sales
X360, PS3, Wii, DS, and PS also ranked among the highest performers
NA leads overall sales across most platforms, followed by EU

Genre Sales

Platform games generated the highest global sales (~$124M), followed by Action (~$117M) and Shooter (~$99M)
Japan shows a strong preference for Role-Playing games
Strategy, Simulation, and Adventure genres showed significantly lower sales

Business Recommendations

Prioritize NA and EU markets for marketing and localization investment
Focus development resources on Platform, Action, Shooter, and Role-Playing genres
Deprioritize low-performing platforms (NG, WS, PCFX, GG, TG16, 3DO) which show near-zero sales across all regions


📁 Repository Structure
📦 video-game-sales-dw
 ┣ 📂 data
 ┃ ┗ 📄 raw_video_game_sales.xlsx
 ┣ 📂 sql
 ┃ ┣ 📄 create_staging_table.sql
 ┃ ┣ 📄 create_dimension_tables.sql
 ┃ ┗ 📄 create_fact_table.sql
 ┣ 📂 ssis
 ┃ ┗ 📄 SSIS_package_notes.md
 ┣ 📂 reports
 ┃ ┗ 📄 VideoGameSales_PivotReport.xlsx
 ┣ 📂 presentation
 ┃ ┗ 📄 VideoGameSales_Presentation.pdf
 ┗ 📄 README.md

🚀 How to Run

Clone the repository
Restore or create the SQL Server database using scripts in /sql
Open SSIS packages in Visual Studio and update connection strings to your local SQL Server instance
Run SSIS packages in order: Staging → Dimensions → Fact Table
Open SSAS project in Visual Studio, connect to your SQL Server, and process the cube
Open the Excel report in /reports and refresh PivotTables to connect to your local data source
