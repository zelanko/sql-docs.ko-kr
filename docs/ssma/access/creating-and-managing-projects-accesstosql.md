---
title: 프로젝트 (AccessToSQL) 만들기 및 관리 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- creating projects
- new projects
- opening projects
- projects
- projects, creating and managing
- saving metadata
- saving projects
ms.assetid: f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 86841e93c16c2a842601c6a3a18601269db0d9bd
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34773359"
---
# <a name="creating-and-managing-projects-accesstosql"></a>프로젝트 (AccessToSQL) 만들기 및 관리
Access 데이터베이스를 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure를 먼저 만들어야 SSMA 프로젝트. 프로젝트는로 마이그레이션하려는 Access 데이터베이스에 대 한 메타 데이터가 포함 된 파일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure로의 대상 인스턴스에 대 한 메타 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure에 마이그레이션된 개체 및 데이터를 받을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 연결 정보 및 프로젝트 설정 합니다.  
  
## <a name="reviewing-default-project-settings"></a>기본 프로젝트 설정 검토  
SSMA는 변환 및 데이터베이스 개체를 동기화 하 고 데이터 변환에 대 한 몇 가지 옵션을 포함 합니다. 이러한 옵션에 대 한 기본 설정은 많은 사용자에 대 한 적절 한입니다. 그러나 새 SSMA 프로젝트를 만들기 전에 옵션 검토를, 하려는 경우, 모든 새 프로젝트에 대 한 사용 될 기본 설정을 변경 합니다.  
  
**기본 프로젝트 설정을 검토 하려면**  
  
1.  에 **도구** 메뉴 선택 **기본 프로젝트 설정**합니다.  
  
2.  프로젝트 형식을 선택 **마이그레이션 대상 버전** 볼 / 변경할 수 있는 설정이 하 고 클릭 한 다음에 대 한 드롭다운 **일반** 탭 합니다.  
  
3.  왼쪽된 창에서 클릭 **변환**합니다.  
  
4.  오른쪽 창에서 옵션을 검토 합니다. 이러한 옵션에 대 한 자세한 내용은 참조 [프로젝트 설정 (변환)](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388)합니다.  
  
5.  필요에 따라 옵션을 변경 합니다.  
  
6.  에 대해 위의 단계를 반복 하는 **마이그레이션**, **GUI**, 및 **유형 매핑** 페이지입니다.  
  
    -   마이그레이션 옵션에 대 한 정보를 참조 하십시오. [프로젝트 설정 (마이그레이션)](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d)합니다.  
  
    -   사용자 인터페이스 옵션에 대 한 정보를 참조 하십시오. [프로젝트 설정 (GUI)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693)합니다.  
  
    -   데이터 형식 매핑 설정에 대 한 자세한 내용은 참조 [프로젝트 설정 (형식 매핑)](http://msdn.microsoft.com/en-us/b87b9683-abed-4677-8c50-18bdba704655)합니다.  
  
    -   SQL Azure 설정에 대 한 정보를 참조 하십시오. [프로젝트 설정 (SQL Azure)](http://msdn.microsoft.com/en-us/bbb8a204-d0e4-4f0b-9709-271feb1f136e)합니다.  
  
**참고** SQL Azure 설정을 SQL Azure로 마이그레이션 프로젝트를 만드는 동안 선택한 경우에 사용할 수는 있습니다.  
  
## <a name="creating-new-projects"></a>새 프로젝트 만들기  
SSMA 기본 프로젝트를 로드 하지 않고 시작 합니다. Access 데이터베이스에서 데이터를 마이그레이션하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 프로젝트 만들기 해야 합니다.  
  
**새 프로젝트를 만들려면**  
  
1.  **파일** 메뉴에서 **새 프로젝트**를 선택합니다.  
  
    **새 프로젝트** 대화 상자가 나타납니다.  
  
2.  **이름** 입력란에 프로젝트 이름을  
  
3.  에 **위치** 입력란에 입력 하거나 프로젝트에 대 한 폴더를 선택 합니다.  
  
4.  마이그레이션에 드롭에서 다운 중 하나를 선택 SQL Server 2005 / SQL Server 2008 / SQL Server 2012 / SQL Server 2014 / SQL Server 2016 / Azure SQL DB, 클릭 하 고 **확인**합니다.  
  
SSMA는 프로젝트 파일을 만듭니다. 이제의 다음 단계를 수행할 수 있습니다 [Access 데이터베이스를 하나 이상의 추가](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)합니다.  
  
## <a name="customizing-project-settings"></a>프로젝트 설정 사용자 지정  
모든 새 SSMA 프로젝트에 적용할 기본 프로젝트 설정을 정의 하는 것 외에도 각 프로젝트에 대 한 설정을 사용자 지정할 수도 있습니다. 자세한 내용은 참조 [설정 변환 및 마이그레이션 옵션](http://msdn.microsoft.com/en-us/0a7304df-2f35-4453-96ef-7ac83dea1167)합니다.  
  
원본 및 대상 데이터베이스 간에 데이터 형식 매핑을 사용자 지정 프로젝트, 데이터베이스 또는 개체 수준에서 매핑 정의할 수 있습니다. 형식 매핑에 대 한 자세한 내용은 참조 [매핑 소스 및 대상 데이터 형식](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)합니다.  
  
## <a name="saving-projects"></a>프로젝트 저장  
프로젝트를 저장 하면 SSMA 프로젝트 설정 및 필요에 따라 프로젝트 파일에는 데이터베이스 메타 데이터를 유지 합니다.  
  
**프로젝트를 저장 하려면**  
  
-   에 **파일** 메뉴 선택 **프로젝트 저장**합니다.  
  
    데이터베이스 프로젝트 내에서 변경 된 변환 하지 않은 경우 SSMA 하 라는 메시지가 나타납니다 프로젝트에 메타 데이터를 저장 합니다. 메타 데이터를 저장 하면 오프 라인으로 작업 합니다. 또한 기술 지원 담당자를 포함 하 여 다른 사용자에 게 전체 프로젝트 파일을 보낼 수 있습니다. 메타 데이터를 저장 하는 메시지가 다음을 수행 합니다.  
  
    1.  상태를 보여 주는 각 데이터베이스에 대해 **메타 데이터 누락**, 데이터베이스 이름 옆에 있는 확인란을 선택 합니다.  
  
        메타 데이터를 저장 하면 몇 분 정도 걸릴 수 있습니다. 이 시점에서 메타 데이터를 저장 하지 않을 경우 모든 확인란을 선택 하지 마십시오.  
  
    2.  **저장**을 클릭합니다.  
  
        SSMA는 액세스 스키마를 구문 분석 하 고 프로젝트 파일에 메타 데이터를 저장 합니다.  
  
## <a name="opening-projects"></a>프로젝트 열기  
프로젝트를 열 때에서 연결이 끊어지도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다. 이렇게 하면 오프 라인으로 작업할 수 있습니다. 메타 데이터 로드 데이터베이스 개체를 업데이트 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다. 에 연결 해야 데이터를 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다.  
  
**프로젝트를 열려면**  
  
1.  다음 절차 중 하나를 사용 합니다.  
  
    -   에 **파일** 메뉴에서 **최근에 사용한 프로젝트**, 한 다음 열려는 프로젝트를 선택 합니다.  
  
    -   에 **파일** 메뉴 선택 **프로젝트 열기**,.a2ssproj 프로젝트 파일, 파일을 찾은 다음 클릭 **열려**합니다.  
  
2.  다시 연결 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]의 **파일** 메뉴 선택 **SQL Server에 다시 연결**합니다.  
  
3.  SQL Azure에 다시 연결 하는 **파일** 메뉴 선택 **SQL Azure에 다시 연결 합니다.**  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계에서는 [하나 이상의 Access 데이터베이스 추가](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)합니다.  
  
## <a name="see-also"></a>관련 항목  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[Access 데이터베이스 파일 추가 및 제거](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)  
  
