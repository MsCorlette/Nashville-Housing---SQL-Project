## Nashville-Housing---SQL-Project
## SQL Data Cleaning guided project
### Data Source:

### Dataset:

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
	  





