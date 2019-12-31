---
title: SQLXML에서 DiffGram에 대한 지침 및 제한 사항
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: eae0b81b3c55a4afe611cd8ed6fdbb495b498c61
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246604"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>SQLXML에서 DiffGram에 대한 지침 및 제한 사항
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  SQLXML 4.0에서 DiffGram을 사용할 때는 다음 사항을 기억해야 합니다.  
  
-   **Text/ntext** 및 images와 같은 BLOB (Binary large object) 형식은 diffgram를 사용 하 여 작업 하는 경우에는 동시성 제어에 사용 하기 위해이를 포함 하기 때문에 ** \<diffgr gr** 에서 사용 하면 안 됩니다. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 BLOB 형식 비교에 대한 제한으로 인해 문제가 발생할 수 있습니다. 예를 들어 LIKE 키워드는 **text** 데이터 형식의 열을 비교 하기 위해 WHERE 절에 사용 됩니다. 그러나 데이터 크기가 8K 보다 큰 BLOB 유형의 경우에는 비교가 실패 합니다.  
  
-   **Ntext** 데이터의 특수 문자는 BLOB 형식 비교에 대 한 제한 사항 때문에 SQLXML 4.0에 문제가 발생할 수 있습니다. 예를 들어 **ntext** 형식의 열에 대 한 동시성 검사에 사용 되는 경우 DiffGram의 "[Serializable]" ** \<** 을 사용 하면 DiffGram의>블록 앞에는 다음 SQLOLEDB 오류 설명과 함께 실패 하 게 됩니다.  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
