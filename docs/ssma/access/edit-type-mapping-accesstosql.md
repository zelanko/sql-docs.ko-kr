---
title: "형식 매핑 (AccessToSQL) 편집 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 7f9d9530-6c04-41d9-bbe7-d91820a30066
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2cfe289d367eee5d33177f8170e4be2919870ada
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="edit-type-mapping-accesstosql"></a>형식 매핑 (AccessToSQL) 편집
**형식 매핑 편집** 대화 상자를 사용 하면 원본 및 대상 데이터베이스 개체 간의 형식이 매핑되는 방법을 지정할 수 있습니다.  
  
여러 위치에서이 대화 상자에 액세스할 수 있습니다.  
  
-   원본 데이터베이스 또는 데이터베이스 개체를 선택 하면는 **유형 매핑** 메타 데이터 탐색기의 오른쪽에 탭이 나타납니다. 클릭 **추가** 는 새로운 형식 매핑을 추가 하거나 클릭 **편집** 기존 형식 매핑을 변경할 수 있습니다.  
  
-   에 **도구** 메뉴 선택 **프로젝트 설정** 또는 **기본 프로젝트 설정**합니다. 결과 대화 상자에서 선택 **유형 매핑**합니다. 클릭 **추가** 는 새로운 형식 매핑을 추가 하거나 클릭 **편집** 기존 형식 매핑을 변경할 수 있습니다.  
  
테이블 관련 형식 매핑을는 프로젝트 형식 매핑 및 데이터베이스를 재정의 합니다. 데이터베이스 관련 매핑을 프로젝트 매핑을 재정의합니다.  
  
## <a name="options"></a>옵션  
**원본 유형**  
원본 데이터 형식에 매핑할 선택는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식입니다.  
  
다음 필드 아래에 표시 됩니다 가변 길이 데이터 형식이 인 경우 **소스 형식**:  
  
**보낸 사람**  
이 매핑에 대 한 최소 길이 지정 합니다. 예를 들어는 **텍스트** 데이터 형식으로 입력할 수 있는 10부터 시작 하는 범위에 대 한이 매핑은 임을 지정 하려면 **text(10)**합니다.  
  
**수행할 작업**  
이 매핑에 대 한 최대 길이 지정 합니다. 예를 들어는 **텍스트** 데이터 형식으로 입력할 수 있는 20 끝 범위에 대 한이 매핑은 임을 지정 하려면 **text(20)**합니다.  
  
**대상 유형**  
선택 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 원본 데이터 형식이 매핑되는 데이터 형식입니다. SSMA는 테이블 또는 저장된 프로시저를 만들 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)],이 데이터 형식으로 원본 데이터 형식이 변경 됩니다.  
  
다음 필드 아래에 표시 됩니다 가변 길이 데이터 형식이 인 경우 **대상 유형**:  
  
**Replace with**  
이 매핑에 대 한 대상 길이 지정 합니다. 예를 들어는 **nvarchar** 데이터 형식으로 입력할 수 있는 지정 된 원본 데이터 형식이에 매핑되고 지정할 수는 20 **nvarchar (20)**합니다.  
  

