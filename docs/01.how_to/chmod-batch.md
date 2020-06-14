# How To Change Permission of File OR Directory in Batch

## Batch Operate with Files

`find -type f -exec chmod 644 {} \;  `

**or**

`find -type f|xargs chmod 644  `

## Batch Operate with Directory

`find -type d -exec chmod 745 {} \;  `

**or**

`find -type d|xargs chmod 745  `
