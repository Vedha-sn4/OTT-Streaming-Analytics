# OTT Streaming Analytics Dashboard 🌐🎬

## Project Overview
This Power BI dashboard transforms raw streaming backend data into actionable business intelligence for a global streaming service. The project establishes an optimized data architecture to monitor platform health, content performance, subscriber behaviors, translation dynamics, and marketing campaign efficiency across multiple international regions.

---

## Datasets & Data Architecture

The project utilizes a high-performance **Star Schema** comprised of seven interconnected datasets. This structure isolates master descriptive attributes from transactional data, minimizing redundancy and maximizing DAX filter performance.

### 1. Central Viewership Log (`Fact_Viewership_And_Ratings`)
* **Dataset Scale:** 120,000 highly granular transactional records capturing individual streaming sessions.
* **Core Attributes:** `fact_id` (PK), `watch_date` (spanning Jan 2024 to June 2026), `watch_time_minutes`, `user_rating` (1.0 to 5.0), and relational foreign keys (`content_id`, `platform_id`, `viewer_id`, `playback_audio_lang_id`, `subtitle_lang_setting`).
* **Analytical Purpose:** Functions as the operational engine of the entire schema. It bridges dimensions together and houses the core business logic tracking viewer-to-content interactions:
    * **Scenario A (Native Match):** Operationalized when a title's original language matches a viewer's preferred language, defaulting the playback track to native and disabling subtitles.
    * **Scenario B (Cross-Language Translation):** Triggered when language backgrounds diverge, dynamically splitting consumption records into **Dubbed Tracks** (65% probability) or **Subtitled Overlays** (35% probability).
    * **KPI Generation:** Serves as the base data source for calculating platform traffic volumes, baseline watch hours, and user satisfaction ratings.

### 2. Subscriber Profiles (`Dim_Viewer`)
* **Dataset Scale:** 5,000 unique customer profiles.
* **Core Attributes:** Age (18–65), gender, subscription tier (Basic, Standard, Premium), geographic location, and preferred native language.
* **Analytical Purpose:** Drives demographic clustering, allowing analysts to segment platform consumption trends by generational cohorts, monetization tiers, and cultural backgrounds.

### 3. Media Catalog (`Dim_Content`)
* **Dataset Scale:** 1,500 distinct titles.
* **Core Attributes:** Asset types (60% Movies / 40% Series), release years (2018–2026), runtimes, primary genres, production country IDs, and original production language IDs.
* **Analytical Purpose:** Evaluates inventory health, tracking which type of content formats, runtimes, and genres generate the highest audience retention and return on investment.

### 4. Language & Geography Masters (`Dim_Language` & `Dim_Geography`)
* **Dataset Scale:** 12 master language classifications and 10 core global market territories.
* **Core Attributes:** Global languages (English, Hindi, Korean, Spanish, etc.), regional Indian tracks (Tamil, Telugu, Malayalam, Bengali), and macro-regional geography definitions.
* **Analytical Purpose:** Essential for tracking global localization and cross-border consumption. The language table handles complex intra-country regional preferences, while the geography table maps global consumption hotspots.

### 5. Platform Channels & Acquisition (`Dim_Platform` & `Dim_Marketing`)
* **Dataset Scale:** 5 streaming delivery channels and 50 campaign acquisition profiles.
* **Core Attributes:** Platform names (Netflix, Prime Video, Disney+ Hotstar, etc.), marketing campaign sources (Social Media, Influencer, Organic, etc.), promo codes, and customer acquisition costs.
* **Analytical Purpose:** Tracks distribution channel effectiveness alongside marketing efficiency, calculating the exact financial return and viewership engagement generated per dollar spent on user acquisition.

---

## Dashboard Page Structure & Business Purpose

### 🖥️ Page 1: Executive Overview & Platform Performance
* **Purpose:** Built for C-suite leadership to track macro platform health. It monitors absolute growth trends, active audience size, and consumption scaling from 2024 through mid-2026 across our primary streaming delivery platforms.

### 🎬 Page 2: Content Catalog & Genre Performance
* **Purpose:** Focused on catalog development and production analytics. This page identifies which genres and formats (Movies vs. Series) maximize user retention, maps runtime optimization thresholds, and highlights which global production hubs deliver the highest quality return on content creation.

### 👥 Page 3: Audience Demographics & Behavioral Analysis
* **Purpose:** Designed for subscriber segmentation. It breaks down the streaming audience by age groups, genders, and regional subscription structures, while specifically visualizing the micro-distribution of diverse native language preferences and cultural cross-border consumption habits.

### 🌐 Page 4: OTT Streaming Analytics (Localization & Translation Insights)
* **Purpose:** Analyzes audience engagement across translation tracks. This page evaluates global demand for domestic native language content versus localized versions, directly comparing user preferences for dubbed audio tracks over subtitled media overlays.

### 📈 Page 5: Marketing Campaigns & Acquisition Efficiency
* **Purpose:** Tailored for marketing analysts to track user acquisition ROI. It evaluates the conversion success of different promotional strategies, calculates media consumption drivers, and maps individual campaign channels on a spending vs. engagement efficiency matrix.

---

## Performance Engineering & Enhancements

To keep the reporting interface completely responsive and fast, the project includes the following technical enhancements:

* **Fact-Table Optimization Columns:** Engineered custom lookup logic directly into the central transaction records. This safely translates raw database integer IDs into clean text strings (such as spoken languages and specific translation styles) without changing table relationships or disrupting the underlying star schema.
* **Core Business Metrics:** Implemented dedicated calculations to track total platform viewership volume, convert raw streaming minutes into global watch hours, evaluate user satisfaction ratings, and aggregate campaign acquisition costs.
