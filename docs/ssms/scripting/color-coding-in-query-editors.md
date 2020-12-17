---
title: 쿼리 편집기에서 코드 색상 지정
description: 특정 텍스트를 더 쉽게 찾을 수 있도록 텍스트 범주를 색으로 구분하는 방법과 사용자 지정 색 구성표를 구성하는 방법을 알아봅니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Editor [SQL Server Management Studio], color coding
- color coding [Query Editor]
ms.assetid: 802882dc-c997-4e3f-8a01-994bb43169ae
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d373506d2824e874442386c27d7aa866984f5d15
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480694"
---
# <a name="color-coding-in-query-editors"></a>쿼리 편집기에서 코드 색상 지정

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

코드 편집기에 입력하는 텍스트에는 범주가 할당되고 각 범주는 색으로 표시됩니다. 색을 통해 코드의 텍스트를 빠르게 찾을 수 있습니다. 예를 들어 주석은 진한 녹색으로 표시됩니다. 다음 표에서는 가장 일반적인 색을 나열합니다. **도구**, **옵션** 메뉴를 사용하여 전체 색 목록과 해당 범주를 볼 수 있으며 사용자 지정 색 구성표를 구성할 수 있습니다. 기본 색을 변경하는 방법은 [Change Font Color, Size, and Style](./change-font-color-size-and-style.md)을 참조하십시오.  
  
## <a name="default-code-colors"></a>기본 코드 색  
  
|색|범주|  
|-----------|--------------|  
|빨강|SQL 문자열|  
|진한 녹색|주석|  
|은색 배경에 검정|SQLCMD 명령|  
|자홍|시스템 함수|  
|녹색|시스템 테이블, 뷰 또는 테이블 반환 함수와 시스템 스키마 sys 및 INFORMATION_SCHEMA|  
|파랑|키워드|  
|청록|줄 번호 또는 템플릿 매개 변수|  
|적갈색|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저|  
|진한 회색|연산자|  
  
## <a name="status-bar"></a>상태 표시줄  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 상태 표시줄에 다른 색상을 사용하도록 개체 탐색기에서 등록된 서버 또는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 서버를 구성할 수 있습니다. 이렇게 하면 동시에 여러 창이 열려 있을 때 각 편집기 창에 연결된 서버를 식별할 수 있습니다. 상태 표시줄 색상 설정에 대한 자세한 내용은 [상태 표시줄&#40;데이터베이스 엔진 쿼리 편집기&#41;](./status-bar-database-engine-query-editor.md)을 참조하세요.  
  
 일부 유형의 편집기에는 상태 표시줄이 표시되지 않으며 여러 색상이 지원되지 않습니다.  
  
