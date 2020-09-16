---
description: 변경 스크립트 저장 대화 상자(Visual Database Tools)
title: 변경 스크립트 저장 대화 상자
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.generatechangescript
- vdtsql.chm:65544
ms.assetid: fc9d1639-5efa-44fe-a04f-4d4d0def2833
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 7388283d4605547a400c284c2499e4f0d9c4db46
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468341"
---
# <a name="save-change-script-dialog-box-visual-database-tools"></a>변경 스크립트 저장 대화 상자(Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
이 대화 상자에는 테이블을 마지막으로 저장한 후에 변경한 내용에 대한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트가 표시됩니다. 이 대화 상자를 사용하여 선택한 위치에 텍스트 파일로 스크립트를 저장할 수도 있습니다.  
  
테이블 디자이너에서 테이블에 대해 변경한 내용을 저장하지 않은 상태에서 이 대화 상자에 액세스할 수 있습니다. **테이블 디자이너** 메뉴에서 **변경 스크립트 생성**을 클릭합니다.  
  
> [!NOTE]  
> Visual Database Tools에서 제공된 변경 스크립트에는 오류 처리가 포함되지 않습니다. 변경 스크립트는 툴이 열린 후에 데이터베이스 개체가 변경되지 않았으므로 변경 관련 문제가 발생하지 않는다고 가정합니다. 변경 스크립트를 실행하기 전에 적절한 오류 처리 문을 포함시켜야 합니다.  
  
## <a name="options"></a>옵션  
**저장할 때마다 자동으로 변경 스크립트 만들기**  
이 옵션을 선택하면 테이블에 변경 내용을 저장할 때마다 **변경 스크립트 저장** 대화 상자가 나타납니다.  
  
**예**  
텍스트 파일의 위치를 선택할 수 있는 **저장** 대화 상자를 엽니다.  
  
**아니요**  
변경 스크립트 작성을 취소합니다.  
  
