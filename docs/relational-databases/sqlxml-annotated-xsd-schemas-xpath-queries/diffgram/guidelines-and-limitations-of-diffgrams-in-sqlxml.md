---
title: "지침 및 SQLXML에서 diffgram에 대 한 제한 사항 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
caps.latest.revision: "7"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8e1830f0cc86c652ce5ecb1a5cf0c0d0a6a76701
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>SQLXML에서 DiffGram에 대한 지침 및 제한 사항
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]SQLXML 4.0에서 Diffgram을 사용할 때 다음을 고려 하세요.  
  
-   이진 대형 개체 (BLOB)와 같은 형식을 **텍스트/ntext** 이미지에서는 사용할 수 없습니다 및는  **\<diffgr: 하기 전에 >** 에서 사용 하기 위해 포함 됩니다이 때문에 Diffgram으로 작업할 때의 블록 동시성 제어입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 BLOB 형식 비교에 대한 제한으로 인해 문제가 발생할 수 있습니다. WHERE 절에 열을 비교 하는 것에 대 한 LIKE 키워드는 사용 하는 예를 들어는 **텍스트** 데이터 형식입니다; 그러나 비교 작업이 실패 합니다 데이터의 크기는 8k 이상이 BLOB 형식입니다.  
  
-   에 특수 문자가 **ntext** 데이터 비교 BLOB 형식에 대 한 제한으로 인해 SQLXML 4.0 문제가 발생할 수 있습니다. 예를 들어, "[serializable]"에서 사용 된  **\<diffgr: 하기 전에 >** 동시성의 열 검사를 수행할 때 DiffGram의 블록 **ntext** 종류는 다음과 같은 SQLOLEDB와 함께 실패 합니다 오류 설명:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
