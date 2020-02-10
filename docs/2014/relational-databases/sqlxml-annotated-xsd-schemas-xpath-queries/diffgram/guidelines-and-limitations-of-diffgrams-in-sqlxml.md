---
title: SQLXML의 Diffgram에 대 한 지침 및 제한 사항 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a1113bf11fcb3b1be2164bc6e685e6454323f3df
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66013057"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>SQLXML에서 DiffGram에 대한 지침 및 제한 사항
  SQLXML 4.0에서 DiffGram을 사용할 때는 다음 사항을 기억해야 합니다.  
  
-   DiffGram으로 작업할 때는 `text/ntext` 및 이미지와 같은 BLOB(Binary Large Object) 형식을 `<diffgr:before>` 블록에 사용하면 안 됩니다. 그 이유는 동시성 제어에 사용하도록 BLOB 형식이 포함될 수 있기 때문입니다. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 BLOB 형식 비교에 대한 제한으로 인해 문제가 발생할 수 있습니다. 예를 들어 LIKE 키워드는 `text` 데이터 형식의 열을 비교하기 위해 WHERE 절에 사용되지만 BLOB 형식의 데이터 크기가 8K 이상이면 비교 작업이 실패합니다.  
  
-   SQLXML 4.0에서는 BLOB 형식 비교에 대한 제한으로 인해 `ntext` 데이터에 특수 문자가 있으면 문제가 발생할 수 있습니다. 예를 들어 `<diffgr:before>` 형식의 열에 대해 동시성 검사를 수행할 때 DiffGram의 `ntext` 블록에 "[Serializable]"을 사용하면 다음과 같은 SQLOLEDB 오류 설명과 함께 작업이 실패합니다.  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
