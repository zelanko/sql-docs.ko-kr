---
description: SQLXML에서 DiffGram에 대한 지침 및 제한 사항
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
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f5d9cbcd08d41f4ce134a663fdcc1cf1bd1c3298
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97415008"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>SQLXML에서 DiffGram에 대한 지침 및 제한 사항
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  SQLXML 4.0에서 DiffGram을 사용할 때는 다음 사항을 기억해야 합니다.  
  
-   Diffgram로 작업할 때 **text/ntext** 및 images와 같은 BLOB (Binary large object) 형식을 블록에 사용 하면 안 **\<diffgr:before>** 됩니다. 동시성 제어에 사용 하기 위해 이러한 형식을 포함 하기 때문입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 BLOB 형식 비교에 대한 제한으로 인해 문제가 발생할 수 있습니다. 예를 들어 LIKE 키워드는 **text** 데이터 형식의 열을 비교 하기 위해 WHERE 절에 사용 됩니다. 그러나 데이터 크기가 8K 보다 큰 BLOB 유형의 경우에는 비교가 실패 합니다.  
  
-   **Ntext** 데이터의 특수 문자는 BLOB 형식 비교에 대 한 제한 사항 때문에 SQLXML 4.0에 문제가 발생할 수 있습니다. 예를 들어 **\<diffgr:before>** **ntext** 형식의 열에 대 한 동시성 검사에 사용 될 때 DiffGram의 블록에 "[Serializable]"을 사용 하면 다음과 같은 SQLOLEDB 오류 설명과 함께 작업이 실패 합니다.  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
