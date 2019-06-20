---
title: 형식 매핑 (MySQLToSQL) 편집 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 184f7ab2-725f-491e-a15b-b889f2fb6a68
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 98b7c0433e506d7ef6e825199a9a6629c52e6f3b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63183090"
---
# <a name="edit-type-mapping-mysqltosql"></a>형식 매핑 편집(MySQLToSQL)
합니다 **형식 매핑 편집** 대화 상자를 사용 하면 원본 및 대상 데이터베이스 개체 간의 형식이 매핑되는 방법을 지정 합니다.  
  
여러 위치에서이 대화 상자에 액세스할 수 있습니다.  
  
-   원본 데이터베이스 또는 데이터베이스 개체를 선택 합니다 **형식 매핑** 메타 데이터 탐색기의 오른쪽에 탭이 표시 됩니다. 클릭 **추가** 하는 새로운 형식 매핑을 추가 하거나 클릭 **편집** 기존 형식 매핑을 변경 합니다.  
  
-   에 **도구** 메뉴에서 **프로젝트 설정** 하거나 **기본 프로젝트 설정**. 선택 대화 상자가 열리면 **형식 매핑**합니다. 클릭 **추가** 하는 새로운 형식 매핑을 추가 하거나 클릭 **편집** 기존 형식 매핑을 변경 합니다.  
  
-   테이블 관련 형식 매핑을는 프로젝트 형식 매핑 및 데이터베이스를 재정의 합니다. 데이터베이스 관련 매핑을 프로젝트 매핑을 재정의합니다.  
  
## <a name="options"></a>변수  
  
##### <a name="source-type"></a>소스 형식  
SQL Server 데이터 형식에 매핑할 원본 데이터 유형을 선택 합니다.  
  
데이터 형식은 가변 길이의 경우 다음 필드를 아래의 나타납니다 **Sourcetype**:  
  
##### <a name="from"></a>보낸 사람  
이 매핑에 대 한 최소 길이 지정 합니다. 예를 들어 합니다 **nchar** 데이터 형식에서 시작 하는 범위에 대 한이 매핑 임을 지정 하려면 10을 입력할 수 있습니다 **nchar(10) 합니다.**  
  
##### <a name="to"></a>수행할 작업  
이 매핑에 대 한 최대 길이 지정 합니다. 예를 들어 합니다 **nchar** 데이터 형식으로이 매핑은 끝 범위를 지정 하는 20을 입력할 수 있습니다 **nchar(20) 합니다.**  
  
##### <a name="target-type"></a>대상 형식  
원본 데이터 형식이 매핑되는 SQL Server 데이터 형식을 선택 합니다. SSMA는 테이블을 만들 때 또는 SQL Server에서이 데이터 형식으로 원본 데이터 형식이 변경 됩니다.  
  
가변 길이 데이터 형식이 인 경우 아래에 다음 필드에 표시 됩니다 **대상 유형**:  
  
##### <a name="replace-with"></a>바꿀 내용  
이 매핑에 대 한 대상 길이 지정 합니다. 예를 들어 합니다 **nvarchar** 데이터 형식으로 지정 된 원본 데이터 형식으로 매핑하도록 지정 하는 20을 입력할 수 있습니다 **nvarchar (20).**  
  
