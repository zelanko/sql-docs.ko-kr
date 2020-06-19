---
title: 유틸리티 관리 (SQL Server 유틸리티) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 3e5a00c3-8905-40f0-9ddc-d924df9c2f0d
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: fca4ea655ffdcf8471d1340016d16f2c5b9c352a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84927694"
---
# <a name="utility-administration-sql-server-utility"></a>유틸리티 관리(SQL Server 유틸리티)
  유틸리티 관리 탭을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티의 정책, 보안 및 데이터 웨어하우스 설정을 관리할 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티 개념에 대한 자세한 내용은 [SQL Server 유틸리티 기능 및 태스크](../relational-databases/manage/sql-server-utility-features-and-tasks.md)를 참조하세요.  
  
## <a name="ui-element-list"></a>UI 요소 목록  
 정책 탭 - 정책 탭을 사용하여 전역 모니터링 정책을 보거나 지정할 수 있습니다.  
  
 전역 데이터 계층 애플리케이션의 모니터링 정책을 설정합니다. 이 옵션의 값 목록을 확장하려면 정책 이름 옆에 있는 화살표를 클릭하거나 정책 제목을 클릭합니다.  
 언제 애플리케이션에서 프로세서 용량이 부족합니까? 이 정책을 변경하려면 정책 설명 오른쪽에 있는 컨트롤을 사용하고 **적용**을 클릭합니다. 아래쪽에 있는 단추를 사용하여 기본값으로 복원하거나 변경을 취소할 수도 있습니다.  
  
-   프로세서 사용률의 기본 최대값은 70%입니다.  
  
-   프로세서 사용률의 기본 최소값은 0%입니다.  
  
 언제 애플리케이션에서 파일 공간이 부족합니까? 데이터 파일이나 로그 파일 공간 사용률에 대한 정책을 변경하려면 정책 설명 오른쪽에 있는 컨트롤을 사용하고 **적용**을 클릭합니다. 아래쪽에 있는 단추를 사용하여 기본값으로 복원하거나 변경을 취소할 수도 있습니다.  
  
-   파일 공간 사용률의 기본 최대값은 70%입니다.  
  
-   파일 공간 사용률의 기본 최소값은 0%입니다.  
  
 전역 SQL Server의 관리되는 인스턴스 애플리케이션 모니터링 정책을 설정합니다. 이 옵션의 값 목록을 확장하려면 정책 이름 옆에 있는 화살표를 클릭하거나 정책 제목을 클릭합니다.  
 언제 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 관리되는 인스턴스에서 프로세서 용량이 부족합니까? 이 정책을 변경하려면 정책 설명 오른쪽에 있는 컨트롤을 사용하고 **적용**을 클릭합니다. 아래쪽에 있는 단추를 사용하여 기본값으로 복원하거나 변경을 취소할 수도 있습니다.  
  
-   인스턴스 프로세서 사용률의 기본 최대값은 70%입니다.  
  
-   인스턴스 프로세서 사용률의 기본 최소값은 0%입니다.  
  
 언제 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 관리되는 인스턴스 컴퓨터에서 프로세서 용량이 부족합니까? 이 정책을 변경하려면 정책 설명 오른쪽에 있는 컨트롤을 사용하고 **적용**을 클릭합니다. 아래쪽에 있는 단추를 사용하여 기본값으로 복원하거나 변경을 취소할 수도 있습니다.  
  
-   컴퓨터 프로세서 사용률의 기본 최대값은 70%입니다.  
  
-   컴퓨터 프로세서 사용률의 기본 최소값은 0%입니다.  
  
 언제 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 관리되는 인스턴스에서 파일 공간이 부족합니까? 데이터 파일이나 로그 파일 공간 사용률에 대한 정책을 변경하려면 정책 설명 오른쪽에 있는 컨트롤을 사용하고 **적용**을 클릭합니다. 아래쪽에 있는 단추를 사용하여 기본값으로 복원하거나 변경을 취소할 수도 있습니다.  
  
-   파일 공간 사용률의 기본 최대값은 70%입니다.  
  
-   파일 공간 사용률의 기본 최소값은 0%입니다.  
  
 언제 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 관리되는 인스턴스 컴퓨터에서 스토리지 볼륨 공간이 부족합니까? 이 정책을 변경하려면 정책 설명 오른쪽에 있는 컨트롤을 사용하고 **적용**을 클릭합니다. 아래쪽에 있는 단추를 사용하여 기본값으로 복원하거나 변경을 취소할 수도 있습니다.  
  
-   컴퓨터 볼륨 공간 사용률의 기본 최대값은 70%입니다.  
  
-   컴퓨터 볼륨 공간 사용률의 기본 최소값은 0%입니다.  
  
 매우 불안정한 리소스에 의해 발생하는 정책 위반 노이즈를 줄입니다. 이 기능의 컨트롤을 확장하려면 오른쪽에 표시되는 아래쪽 화살표를 클릭합니다.  
 자세한 내용은 [CPU 사용 정책에서 노이즈 줄이기 &#40;SQL Server 유틸리티](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md) 를 참조 하세요&#41;  
  
## <a name="ui-element-list"></a>UI 요소 목록  
 보안 탭 - UCP를 관리하거나 읽을 수 있는 권한이 있는 로그인 이름을 표시합니다.  
  
 Utility 읽기 역할에 추가될 UCP에서 로그인을 선택합니다.  
 Utility 읽기 권한이 있는 사용자 계정으로 다음과 같은 작업을 할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티에 연결합니다.  
  
-   SSMS의 유틸리티 탐색기에서 모든 뷰포인트를 봅니다.  
  
-   SSMS의 유틸리티 탐색기의 유틸리티 관리 노드에 있는 설정을 봅니다.  
  
 유틸리티 관리자는 SQL Server Utility에 SQL Server 인스턴스를 등록하거나 제거할 수 있으며 관리되는 인스턴스의 정책을 수정하고 UCP의 관리 설정을 수정할 수 있습니다.  
  
 유틸리티 관리자가 되려면 SQL Server 인스턴스에 대한 sysadmin 권한이 있어야 합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] UCP에 대한 사용자 계정을 추가하거나 변경하려면 SSMS의 개체 탐색기를 사용하여 SQL Server UCP 인스턴스의 서버 로그인에 사용자를 추가합니다. 자세한 내용은 [sp_addlogin&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogin-transact-sql)을 참조하세요.  
  
## <a name="ui-element-list"></a>UI 요소 목록  
 데이터 웨어하우스 탭 - 유틸리티 관리 데이터 웨어하우스에 대한 구성 세부 정보를 표시합니다.  
  
 데이터 보존  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 관리되는 인스턴스에 대해 수집된 사용률 정보의 데이터 보존 기간을 지정합니다. 기본 기간은 1년입니다. 최소값은 1개월입니다. 지원되는 가장 긴 기간은 2년입니다.  
  
 유틸리티 데이터 웨어하우스 구성 정보  
 다음 구성 설정은 이 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]릴리스에서 구성할 수 없습니다.  
  
-   UMDW name: Sysutility_mdw_ \<GUID> _DATA입니다.  
  
-   컬렉션 집합 업로드 빈도: 15분마다.  
  
 UMDW 디렉터리는 구성 가능 합니다.: \<System drive> Files\Microsoft SQL Server \ MSSQL10_50. <UCP_Name> \mssql\data입니다. \\ 여기서 \<System drive> 는 일반적으로 C:\입니다. 드라이브나. 로그 파일 UMDW_ _LOG는 \<GUID> 동일한 디렉터리에 있습니다.  
  
> [!NOTE]  
>  UMDW(sysutility_mdw) 파일 위치는 detach/attach 또는 ALTER DATABASE를 사용하여 변경할 수 있으며 ALTER DATABASE를 사용하는 것이 좋습니다. 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)를 참조하세요.  
  
 제품 기본값으로 돌아갑니다.  
 이 탭의 설정을 기본값으로 다시 설정하려면 **기본값 복원** 단추를 클릭하고 **적용**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [유틸리티 대시보드 &#40;SQL Server 유틸리티&#41;](../../2014/database-engine/utility-dashboard-sql-server-utility.md)   
 [배포 된 데이터 계층 응용 프로그램 세부 정보 &#40;SQL Server 유틸리티&#41;](../../2014/database-engine/deployed-data-tier-application-details-sql-server-utility.md)   
 [Managed Instance 세부 정보 &#40;SQL Server 유틸리티&#41;](../../2014/database-engine/managed-instance-details-sql-server-utility.md)   
 [SQL Server 유틸리티에서 SQL Server 인스턴스 모니터링](../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)  
  
  
