## Nashville-Housing---SQL-Project
## SQL Data Cleaning guided project
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

2.  Populate Property Address

SELECT a.ParcelID,a.PropertyAddress, b.ParcelID, b.PropertyAddress, Coalesce(a.PropertyAddress, b.PropertyAddress) as PopulatedAdress
FROM dbo.[Nashville Housing Data] a
JOIN dbo.[Nashville Housing Data] b
	ON a.ParcelID = b.ParcelID
	AND a.[UniqueID ] <> b.[UniqueID ]
WHERE a.PropertyAddress is null

UPDATE a
SET a.PropertyAddress = b.PropertyAddress
FROM dbo.[Nashville Housing Data] a
JOIN dbo.[Nashville Housing Data] b
	ON a.ParcelID = b.ParcelID
	AND a.[UniqueID ] <> b.[UniqueID ]
WHERE a.PropertyAddress is null

3.  Change Y and N to Yes and No in "Sold as Vacant" field

Select Distinct(SoldAsVacant),COUNT(SoldAsVacant)
From dbo.[Nashville Housing Data]
group by SoldAsVacant
Order by 2

Select SoldAsVacant
,CASE WHEN SoldAsVacant = 'Y' THEN 'Yes'
      WHEN SoldAsVacant = 'N' THEN 'No'
	  ELSE SoldAsVacant
	  END
From dbo.[Nashville Housing Data]

Update dbo.[Nashville Housing Data]
set SoldAsVacant = CASE WHEN SoldAsVacant = 'Y' THEN 'Yes'
      WHEN SoldAsVacant = 'N' THEN 'No'
	  ELSE SoldAsVacant

4.   Remove Duplicates

WITH RowNumCTE as(
Select *,
	ROW_NUMBER() Over (
	Partition by ParcelId,
	PropertyAddress,
	SaleDate,
	SalePrice,
	LegalReference
	Order by
	UniqueId) as row_num
from dbo.[Nashville Housing Data]
)

Select *
from RowNumCTE 
Where row_num > 1

5.  Delete Unsude Columns

Select*
From dbo.[Nashville Housing Data]

Alter Table dbo.[Nashville Housing Data]
Drop Column OwnerAddress, TaxDistrict, PropertyAddress

Alter Table dbo.[Nashville Housing Data]
Drop Column SaleDate

6.
	  





