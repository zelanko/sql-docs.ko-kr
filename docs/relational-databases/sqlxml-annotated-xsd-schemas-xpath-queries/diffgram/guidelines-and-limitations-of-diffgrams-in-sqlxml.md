---
title: 지침 및 SQLXML에 Diffgram의 제한 | Microsoft 문서
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5d0f0ddb4d66aad9280462cf4db595b356e0dc76
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43110395"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>SQLXML에서 DiffGram에 대한 지침 및 제한 사항
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  SQLXML 4.0에서 DiffGram을 사용할 때는 다음 사항을 기억해야 합니다.  
  
-   이진 대형 개체 (BLOB)와 같은 형식 **텍스트/ntext** 이미지에서 사용할 수 없습니다는  **\<diffgr: 하기 전에 >** 블록 DiffGrams을 사용 하는 경우 여기에 해당 용도로 때문에 동시성 제어 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 BLOB 형식 비교에 대한 제한으로 인해 문제가 발생할 수 있습니다. 예를 들어 LIKE 키워드는 WHERE 절에 열을 비교 합니다 **텍스트** 데이터 형식입니다; 그러나 비교 작업이 실패 BLOB 형식의 데이터 크기가 8k 이상이 있습니다.  
  
-   에 특수 문자가 **ntext** 데이터 비교 BLOB 유형에 대 한 제한으로 인해 SQLXML 4.0을 사용 하 여 문제를 발생할 수 있습니다. 예를 들어, "[serializable]"에서 사용 합니다  **\<diffgr: 전에 >** 동시성 검사의 열에 사용 되는 경우 DiffGram의 블록 **ntext** 형식 다음 SQLOLEDB를 사용 하 여 실패 오류 설명:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
