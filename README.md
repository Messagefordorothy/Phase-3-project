TANZANIA WATER WELL STATUS AND DISTRIBUTION: A PREDICTIVE ANALYSIS
Overview
Tanzania, officially the United Republic of Tanzania, is a country in East Africa within the African Great Lakes region. It boasts a rich tapestry of geographical features, bordering Uganda to the northwest; Kenya to the northeast; the Indian Ocean to the east; Mozambique and Malawi to the south; Zambia to the southwest; and Rwanda, Burundi, and the Democratic Republic of the Congo to the west. Mount Kilimanjaro, Africa's highest mountain, stands proudly in northeastern Tanzania. With a population of nearly 62 million according to the 2022 national census, Tanzania is the most populous country located entirely south of the equator. Beyond its size and geographical diversity, Tanzania is a land of cultural richness. The country is home to over 120 ethnic groups, each with its own unique traditions and languages. Swahili, a Bantu language with Arabic influences, serves as the national language and lingua franca, uniting the people.

Tanzania is religiously diverse as well, with Christianity being the largest religion, followed by Islam and traditional African religions. Tanzania is a haven for wildlife enthusiasts. Its vast wilderness areas include the world-renowned Serengeti National Park, famous for the annual Great Migration of millions of wildebeest and zebra. The Ngorongoro Crater, a UNESCO World Heritage Site, shelters a unique ecosystem teeming with wildlife. Offshore, the spice island of Zanzibar offers a glimpse into Tanzania's historical ties with the Arab world, while Mafia Island boasts a marine park known for its stunning coral reefs and gentle giants, the whale sharks.

Access to clean water varies greatly across Tanzania. While urban areas have seen increased access to piped water, a significant portion of the rural population relies on groundwater sources. Many communities depend on wells, boreholes, and springs for their daily needs.

The uneven distribution of water resources, coupled with seasonal variations in rainfall, can create challenges, particularly in arid and semi-arid regions. Government initiatives and NGO efforts are working to improve water infrastructure and expand access to clean water for all Tanzanians. Research Statement

This project aims to delve deeper into the water issues faced by Tanzania. A key challenge lies in ensuring the functionality of water wells, which are vital for many rural communities.

By leveraging machine learning, we propose the development of an algorithm that can predict the functionality of a water well. This algorithm will be designed to classify wells into three categories: functional, non-functional, and functional but requiring repair.

This information can be a powerful tool for prioritizing maintenance efforts and ensuring a more reliable water supply for Tanzanian communities. Research Objectives

In an effort to enhance the management and sustainability of water resources, this research focuses on two key objectives.

Major Decisions During Data cleaning
image

• To find out the geographical distribution of the three classes of water pumps, to help inform which regions need more attention in terms of repair, maintenance, and replacement.

• To build a Machine Learning classifier that will predict the condition of a water well (functional, functional-but-needs-repair, and non-functional), using data such as the kind of pump, when it was installed, the installer, the region, and so on. Research questions

To guide this research, two central questions are posed.

• What is the geographical distribution of the three classes of water pumps, and which regions need more attention for repair, maintenance, and replacement?

• How can a Machine Learning classifier be developed to accurately predict the condition of water wells using data such as pump type, installation date, installer, and region?

Data Understanding
This DataFrame contains 59,400 entries and 40 columns, each representing a different attribute of the data. The columns include various data types: integers (int64), floating-point numbers (float64), and strings (object). Key columns include 'id', 'amount_tsh' (total static head), 'date_recorded', 'funder', 'gps_height', 'installer', 'longitude', 'latitude', 'wpt_name' (waterpoint name), 'population', 'public_meeting', 'scheme_management', and 'scheme_name'. Some columns have missing values, such as 'funder', 'installer', 'public_meeting', 'scheme_management', and 'scheme_name', indicated by the non-null count being less than 59,400. The data appears to be related to water points, likely including information on their location, management, and operational details.

Handling Outliers
Longitudes had outliers
Based on the map below, some points are not located in Tanzania. Tanzania is situated at approximately latitude 6°23′31.20″ South and longitude 35°00′07.20″ East. Therefore, coordinates such as longitude 0.000000 and latitude -2.000000e-08 are not within Tanzania's boundaries. There are about 1,671 data entries with these coordinates. The decision was made to remove these points from the dataset because they do not correspond to locations within Tanzania. The data points are only 3.22 percent of the total dataset and therefore, they can be removed.

Categorical columns to drop 
• Date_recorded - This column is redundant because we already have the 'year of construction' which provides similar temporal information. Thus, 'Date_recorded' can be dropped.

• Funder - Since 'Funder' and 'Installer' contain the same values and 'Installer' has a higher influence on how a water pump functions, you should drop the 'Funder' column.

• Iga, Ward, sub_village - These can be effectively represented by the 'region' column, allowing you to drop 'Iga', 'Ward', and 'sub_village' to reduce redundancy.

• Recorded_by - This column contains uniform information (e.g., 'GeoData Consultants Ltd') across all entries, providing no variability or additional insights, hence it can be dropped.

• Scheme_name - Due to its high number of unique and missing values, 'scheme_name' can be dropped as it may complicate the model without adding significant value.

• Payment - 'Payment' and 'Payment_type' are duplicative as they contain similar values. You can drop 'Payment' to eliminate redundancy.

• Quality_group - Similar to 'water_quality', this column does not add additional information since both describe water quality. Therefore, 'Quality_group' can be dropped.

• Extraction_type, extraction_type_group - These are duplicates to the information in 'Extraction_type_class'. Therefore, retain 'Extraction_type_class' and drop 'Extraction_type'.

• Quantity_group - As it mirrors the values in 'Quantity', you can drop 'Quantity_group' to streamline the dataset.

• Source, Source_type - These columns are duplicative and can be consolidated under 'Source_class', allowing you to drop 'Source' and 'Source_type'.

• Wpt_name - This column has a large number of unique and missing values, which could lead to high dimensionality without much predictive power. It can be dropped.

• Waterpoint_type - Can be represented by 'Waterpoint_type_group', thus 'Waterpoint_type' can be dropped to simplify the model.

• Management- management is a category of the management_group and hence it does not add value to the model
