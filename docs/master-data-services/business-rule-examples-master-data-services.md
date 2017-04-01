---
title: "비즈니스 규칙의 예(Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "01/05/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3974b9be-4b7c-4a37-ab26-1a36ef455744
caps.latest.revision: 21
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 19
---
# 비즈니스 규칙의 예(Master Data Services)
이 문서에서는 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]에 대한 비즈니스 규칙의 예를 보여 줍니다. [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 설치에 포함된 샘플 모델에서 이러한 예를 찾을 수 있습니다.   
  
샘플 모델을 배포하는 방법에 대한 지침은 [Master Data Services](../sql-server/media/master-data-services.png#deploySample)를 참조하세요.  
  
  
## 비즈니스 규칙의 예  
샘플 모델 |엔터티  |비즈니스 규칙 이름| Description  
---------|---------|---------|-----------|  
Customer    | Customer   | Person pmt terms| 고객에 대한 기본 지불 조건을 지정합니다.          
다음 비즈니스 규칙에서 CustomerType 특성 값이 `is equal` [규칙 조건](../master-data-services/business-rule-conditions-master-data-services.md)을 충족하면 `defaults to` [규칙 작업](../master-data-services/business-rule-conditions-master-data-services.md)이 PaymentTerms 특성에 적용됩니다. 충족하지 않으면 아무 작업도 수행되지 않습니다.  
```  
If  
    CustomerType is equal to 2  
Then  
    PaymentTerms defaults to CASH  
Else  
    None      
```  
  
**--------------------------------------------------**  
  
샘플 모델  |엔터티  |비즈니스 규칙 이름|Description    
---------|---------|---------|---------------  
Customer     | Customer    | Org pmt terms | 조직에 대한 기본 지불 조건을 지정합니다.         
다음 비즈니스 규칙에서 CustomerType 특성 값이 `is equal` [규칙 조건](../master-data-services/business-rule-conditions-master-data-services.md)을 충족하면 `defaults to` [규칙 작업](../master-data-services/business-rule-actions-master-data-services.md)이 PaymentTerms 특성에 적용됩니다. 충족하지 않으면 아무 작업도 수행되지 않습니다.  
```  
If  
    CustomerType is equal to 1  
Then  
    PaymentTerms defaults to 210Net30  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
샘플 모델  |엔터티  |비즈니스 규칙 이름| Description    
---------|---------|---------|-----------  
Product     |  Product       | DaysToManufacture |사내 제조에 대한 제조일의 범위를 지정합니다.          
다음 비즈니스 규칙에서 InHouseManufacture 특성 값이 `is equal` [규칙 조건](../master-data-services/business-rule-conditions-master-data-services.md)을 충족하면 `must be between` [규칙 작업](../master-data-services/business-rule-actions-master-data-services.md)이 DaysToManufacture 특성에 적용됩니다. 충족하지 않으면 아무 작업도 수행되지 않습니다.  
```  
If  
    InHouseManufacture is equal to Y  
Then  
    DaysToManufacture must be between 1 and 10  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
샘플 모델  |엔터티  |비즈니스 규칙 이름|Description    
---------|---------|---------|-------------  
Product     |Product         |Required fields| 제품 엔터티 멤버에 대한 필수 특성을 지정합니다.           
다음 비즈니스 규칙에서 모든 조건의 `is required` [유효성 검사 작업](../master-data-services/business-rule-actions-master-data-services.md)은 지정한 특성에 대해 수행됩니다. 특성 값은 Null 또는 공백일 수 없습니다.  
```  
If  
    None  
Then  
    Name is required  
    ProductSubCategory is required  
    Color is required  
    StandardCost is required  
    SafetyStockLevel is required  
    ReorderPoint is required  
    InHouseManufacture is required  
    SellStartDate is required  
    FinishedGoodIndicator is required  
    ProductLine is required  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
샘플 모델  |엔터티  |비즈니스 규칙 이름|Description    
---------|---------|---------|-----------  
Product     | Product        |  Std Cost| 표준 원가가 0보다 크도록 요구합니다.        
다음 비즈니스 규칙에서 모든 조건의 `must be greater than` [규칙 작업](../master-data-services/business-rule-actions-master-data-services.md)은 제품의 StandardCost 특성에 적용됩니다.  
```  
If  
    None  
Then  
    StandardCost must be greater than 0  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
샘플 모델  |엔터티  |비즈니스 규칙 이름|Description    
---------|---------|---------|------------  
Product     | Product        | FG MSRP Cost|제품이 완제품인 경우 MSRP(제조업체 제시 소매 가격) 및 총판 원가가 0보다 크도록 지정합니다.           
  
다음 비즈니스 규칙에서 FinishedGoodIndicator 특성 값이 `is equal` [규칙 조건](../master-data-services/business-rule-conditions-master-data-services.md)을 충족하면 `must be greater than` [규칙 작업](../master-data-services/business-rule-actions-master-data-services.md)이 MSRP 및 DealerCost 특성에 적용됩니다.  
```  
If  
    FinishedGoodIndicator is equal to Y  
Then  
    MSRP must be greater than 0  
    DealerCost must be greater than 0  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
샘플 모델  |엔터티  |비즈니스 규칙 이름|Description    
---------|---------|---------|------------  
Product     | Product        |  Default Name| Color 및 Class 특성 값에 따라 기본 제품 이름을 지정합니다. Color 특성 값이 YLO가 아니고 Class 특성이 NA가 아니면 기본 이름은 Yellow NA입니다.         
다음 비즈니스 규칙에서 Color 및 Class 특성이 `is equal`규칙 조건을 충족하지 않으면 `defaults to`[[규칙 작업](../master-data-services/business-rule-actions-master-data-services.md)](Business%20Rule%20Conditions%20(Master%20Data%20Services).xml)이 Name 특성에 적용됩니다.  
```  
If  
    (Color is equal to YLO AND Class is equal to NA) is not true  
Then  
    Name defaults to Yellow NA  
Else  
    Name defaults to Other  
```  
  
**--------------------------------------------------**  
  
  
**샘플 모델에 있는 비즈니스 규칙의 예를 보려면**  
1. MDS를 설치한 후 설정한 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 웹 사이트로 이동한 다음 **시스템 관리** 상자를 클릭합니다.   
웹 사이트를 설정하는 방법에 대한 지침은 [Master Data Services](../sql-server/media/master-data-services.png)를 참조하세요.  
2. 위의 표에 나열된 비즈니스 규칙을 포함하는 샘플 모델을 클릭한 다음 **엔터티**를 클릭합니다.  
3. 위의 표에 나열된 규칙이 적용되는 엔터티를 클릭한 다음 **비즈니스 규칙**을 클릭합니다.  
4. 보려는 비즈니스 규칙의 이름을 클릭합니다. UI가 확장되고 **If**, **Then** 및 **Else** 문이 표시됩니다.  
  
## 이 문서가 도움이 되었나요? 여러분의 의견을 환영합니다.   
어떤 정보를 찾고 계세요? 정보를 찾으셨나요? 여러분의 의견은 문서의 내용을 개선하는 데 많은 도움이 됩니다. 의견이 있으면 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com)으로 보내 주세요.   
  
  
  
  
