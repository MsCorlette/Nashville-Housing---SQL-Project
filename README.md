## SQL Data Cleaning guided project

## Project Overview


### Data Source: Github.com

### Dataset: 
[https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbnNuQmZtbUNsR2owR1JiRTF1SlVKT0s5YVM3QXxBQ3Jtc0ttZm55ZGdyVWpxanZ4MlpqamdpZ2F1QjhCRFM2LVloQzM4eGFYaWMxZFFTa3lCRExfbngweUx1SjQzallMMkJHcDF3M19zdkhLMEZLRWYyNl9FbmdYeEZhUHB1Ukw1Mi1IOXdNNXhaUERtMTVkWWhLUQ&q=https%3A%2F%2Fgithub.com%2FAlexTheAnalyst%2FPortfolioProjects%2Fblob%2Fmain%2FNashville%2520Housing%2520Data%2520for%2520Data%2520Cleaning.xlsx&v=8rO7ztF4NtU]

### Data Cleaning Process:

1.  Standardizing date format

    SELECT SaleDateConverted, Convert(Date,SaleDate)

    FROM dbo.[Nashville Housing Data]


    UPDATE dbo.[Nashville Housing Data]

    SET SaleDate = Convert(Date,SaleDate)


    ALTER TABLE dbo.[Nashville Housing Data]

    ADD SaleDateConverted Date


    UPDATE dbo.[Nashville Housing Data]

    SET SaleDateConverted  = Convert(Date,SaleDate) 

	  





