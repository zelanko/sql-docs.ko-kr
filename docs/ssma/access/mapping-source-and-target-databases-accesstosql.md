---
title: "원본 및 대상 데이터베이스 (AccessToSQL) 매핑 | Microsoft Docs"
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
helpviewer_keywords:
- database schemas
- mapping, databases
- schemas, mapping to
- schemas, SQL Azure
- schemas, SQL Server
- source database
- target database
ms.assetid: 69bee937-7b2c-49ee-8866-7518c683fad4
caps.latest.revision: 17
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8bc9bde868aa615c2e78ace576394a9d1f782e3e
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="mapping-source-and-target-databases-accesstosql"></a>원본 및 대상 데이터베이스 (AccessToSQL) 매핑
에 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 마이그레이션에 대상 데이터베이스를 지정 해야 합니다. Access 데이터베이스를 여러 개 있는 경우를 다중 매핑할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 (또는 스키마) 또는 연결 된 SQL Azure 데이터베이스에서 여러 스키마입니다.  
  
## <a name="sql-server-or-sql-azure-database-schemas"></a>SQL Server 또는 SQL Azure 데이터베이스 스키마  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]데이터베이스는 스키마의 개념을 사용 하 여 데이터베이스 내의 개체를 논리 그룹으로 구분 합니다. 예를 들어, 라이브러리 데이터베이스 라는 세 개의 스키마를 사용할 수 **설명서**, **오디오**, 및 **비디오** 서로 책, 오디오 및 비디오 개체를 구분 하 합니다. 기본적으로 access 데이터베이스에 매핑되어 **마스터** 데이터베이스 및 **dbo** 스키마에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 와 연결 된 데이터베이스 및 **dbo** SQL Azure의 스키마입니다.  
  
각 Access 데이터베이스 간의 매핑을 사용자 지정 하지 않으면 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스와 스키마를 스키마와 매핑된 기본 데이터베이스를 access 데이터베이스와 관련 된 데이터를 모든 SSMA 마이그레이션됩니다.  
  
## <a name="modifying-the-target-database-and-schema"></a>대상 데이터베이스 및 스키마를 수정합니다.  
SSMA를 각 Access 데이터베이스에 매핑할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 데이터베이스 및 스키마입니다. 다음 절차에는 데이터베이스당 매핑을 사용자 지정 하는 방법을 설명 합니다.  
  
**대상 데이터베이스 및 스키마를 수정 하려면**  
  
1.  액세스 메타 데이터 탐색기 창에서 선택 **메타 데이터를 액세스할**합니다.  
  
    스키마 매핑 역시 사용할 수 있는 선택 된 **데이터베이스** 노드 또는 모든 데이터베이스 노드. 선택한 개체에 대 한 스키마 매핑 목록은 사용자 지정 합니다.  
  
2.  오른쪽 창에서 클릭 하 고 **스키마 매핑** 탭 합니다.  
  
    액세스를 포함 하는 테이블을 보게 데이터베이스 이름 및 해당 ssNoVersion 또는 Sql Azure 스키마입니다. 대상 스키마의 두 부분으로 구성 표기법 (database.schema)으로 표시 됩니다.  
  
3.  사용자 지정 하 고 클릭 하려는 매핑을 포함 하는 행 선택 **수정**합니다.  
  
4.  에 **대상 스키마 선택** 대화 상자에서 검색할 수 있습니다. 사용 가능한 대상 데이터베이스 및 스키마 또는 두 부분으로 구성 표기법 (database.schema)의 텍스트 상자에 이름을 지정 하 고 클릭 한 다음 데이터베이스 및 스키마 형식에 대 한 **확인**합니다.  
  
**매핑 모드**  
  
-   SQL Server에 매핑  
  
원본 데이터베이스는 대상 데이터베이스에 매핑할 수 있습니다. 기본적으로 원본 데이터베이스 매핑된 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSMA를 사용 하 여 연결가 있는 데이터베이스입니다. 매핑되는 대상 데이터베이스에 존재 하지 않는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]를 묻는 메시지를 사용 하는 다음 **"데이터베이스 및/또는 스키마 대상에 존재 하지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터입니다. 해당 하는 동기화 하는 동안 만들어졌습니다. 마십시오 계속 하 시겠습니까 "?** 예를 클릭 합니다. 마찬가지로, 대상에서 존재 하지 않는 스키마를 스키마를 매핑할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 동기화 중에 생성 되는 데이터베이스입니다.  
  
-   SQL Azure에 매핑  
  
연결 된 대상에 원본 데이터베이스를 매핑할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 또는 연결 된 대상에 어떤 스키마 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다. 연결 된 대상 데이터베이스에서 어떤 존재 하지 않는 스키마 소스 스키마를 매핑할 경우 다음 메시지와 함께 나타납니다 **"스키마 대상 메타 데이터에는 존재 하지 않습니다. 해당 하는 동기화 하는 동안 만들어졌습니다. 계속 하 시겠습니까? "** 예를 클릭 합니다.  
  
## <a name="reverting-to-your-initial-database-and-schema"></a>초기 데이터베이스 및 스키마 되돌리기  
Access 데이터베이스 간의 매핑을 사용자 지정 하는 경우와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SQL Azure 데이터베이스와 스키마를 또는에 연결 하는 경우 지정한 데이터베이스에 다시 매핑 되돌릴 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다.  
  
**기본 데이터베이스 및 스키마를 다시 설정 하려면**  
  
1.  스키마 매핑 탭에서 모든 행을 선택 하 고 클릭 **기본값으로 재설정** 기본 데이터베이스 및 스키마에 되돌릴 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [데이터베이스 개체를 변환 합니다.](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  

