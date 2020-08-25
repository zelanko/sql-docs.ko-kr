---
description: 기존 레코드 편집
title: 기존 레코드 편집 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], existing records
ms.assetid: 17ce1263-5897-452a-9ea5-c7f96b33df65
author: rothja
ms.author: jroth
ms.openlocfilehash: 9514e727b416935924e3549e2fa10524bab22bd1
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806136"
---
# <a name="editing-existing-records"></a>기존 레코드 편집
기존 레코드를 편집 하려면 편집 하려는 행으로 이동 하 여 변경할 필드의 **Value** 속성을 변경 합니다. **Field** 개체의 **Value** 속성에 대 한 자세한 내용은 [데이터 검사](./examining-data.md)를 참조 하십시오. 커서 유형에 따라 **업데이트** 또는 **UpdateBatch** 를 사용 하 여 변경 내용을 다시 데이터 원본으로 보냅니다. 자세한 내용은 [데이터 업데이트 및 유지](./updating-and-persisting-data.md)를 참조 하세요.  
  
 저장 프로시저에서 커서를 만들 필요가 없기 때문에 일반적으로 명령 개체와 함께 저장 프로시저를 사용 하 여 업데이트를 수행 하 고 다른 작업을 수행 하는 것이 더 효율적입니다. 커서에 대 한 자세한 내용은 [커서 및 잠금 이해](./understanding-cursors-and-locks.md)를 참조 하세요.