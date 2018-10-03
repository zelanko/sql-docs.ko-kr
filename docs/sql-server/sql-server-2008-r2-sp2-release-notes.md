---
title: SQL Server 2008 R2 SP2 릴리스 정보 | Microsoft 문서
ms.prod: sql
ms.technology: install
ms.custom: ''
ms.date: 01/31/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server 2008 R2 SP2
- Release Notes, SQL Server 2008 R2 SP2
ms.assetid: e2bd3de7-674c-4ea7-8d53-bb40bba86fae
author: craigg-msft
ms.author: craigg
manager: jhubbard
monikerRange: = sql-server-2014 || = sqlallproducts-allversions
ms.openlocfilehash: 029f12681c5409a21d2126dda622656783c76979
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47750321"
---
# <a name="sql-server-2008-r2-sp2-release-notes"></a>SQL Server 2008 R2 SP2 Release Notes
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
이 릴리스 정보 문서에서는 Microsoft SQL Server 2008 R2 서비스 팩 2를 설치하거나 문제를 해결하기 전에 읽어야 할 알려진 문제에 대해 설명합니다. 이 릴리스 정보 문서는 SQL Server 2008 R2 SP2의 모든 버전에 적용되며 온라인으로만 볼 수 있습니다. 문서는 주기적으로 업데이트됩니다.  
  
## <a name="10-whats-new-in-service-pack-2"></a>1.0 서비스 팩 2의 새로운 기능  
DMV(동적 관리 뷰) **sys.dm_db_stats_properties**. 이 DMV를 사용하여 지정된 테이블 또는 현재 데이터베이스에 있는 인덱싱된 뷰에 대한 통계 속성을 반환할 수 있습니다. 예를 들어, 이 DMV는 샘플링된 행 수와 히스토그램에 있는 단계 수를 반환합니다.  
  
## <a name="20-before-you-install"></a>2.0 설치 전 준비 사항  
[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 업데이트 설치 방법에 대한 자세한 내용은 [SQL Server 2008 R2 서비스 설명서](http://msdn.microsoft.com/library/dd638062(SQL.105).aspx)를 참조하세요.  
  
SQL Server 2008 R2를 시작하고 설치하는 방법은 SQL Server 2008 R2 추가 정보를 참조하십시오. 이 추가 정보 문서는 설치 미디어에서 다운로드할 수 있습니다. 또한 [SQL Server 온라인 설명서](sql-server-technical-documentation.md) 및 [SQL Server 포럼](http://social.msdn.microsoft.com/Forums/category/sqlserver/)에서 자세한 내용을 볼 수 있습니다.  
  
### <a name="21-choose-the-correct-file-to-download-and-install"></a>2.1 다운로드 및 설치할 올바른 파일 선택  
다음 표를 사용하여 다운로드 및 설치할 파일을 결정합니다. 서비스 팩을 설치하기 전에 올바른 시스템 요구 사항을 갖추고 있는지 확인합니다. 시스템 요구 사항은 표에 링크되어 있는 다운로드 페이지에서 확인할 수 있습니다.  
  
|현재 설치된 버전|원하는 작업|다운로드 및 설치할 파일|  
|-------------------------------------------|----------------------|---------------------------|  
|32비트 버전의 SQL Server 2008 R2 또는 SQL Server 2008 R2 SP1|32비트 버전의 SQL Server 2008 R2 SP2로 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkId=251790)에서 SQLServer2008R2SP2-KB2630458-x86-ENU 다운로드|  
|32비트 버전의 SQL Server 2008 R2 RTM Express 또는 SQL Server 2008 R2 SP1 Express|32비트 버전의 SQL Server 2008 R2 SP2로 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkId=251790)에 있는 SQLServer2008R2SP2-KB2630458-x86-ENU.exe|  
|32비트 버전의 SQL Server 2008 R2 또는 SQL Server 2008 R2 SP1 클라이언트 및 관리 효율성 도구(SQL Server 2008 R2 Management Studio 포함)|32비트 버전의 SQL Server 2008 R2 SP2로 클라이언트 및 관리 효율성 도구 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkId=251790)에 있는 SQLServer2008R2SP2-KB2630458-x86-ENU.exe|  
|32비트 버전의 SQL Server 2008 R2 Management Studio Express 또는 SQL Server 2008 R2 SP1 Management Studio Express|32비트 버전의 SQL Server 2008 R2 SP2 Management Studio Express로 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkId=251791)에 있는 SQLManagementStudio_x86_ENU.exe|  
|32비트 버전 SQL Server 2008 R2 또는 SQL Server 2008 R2 SP1의 모든 버전 **및** 32비트 버전의 클라이언트 및 관리 도구(SQL Server 2008 R2 RTM Management Studio 포함)|32비트 버전의 SQL Server 2008 R2 SP2로 모든 제품 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkId=251790)에 있는 SQLServer2008R2SP2-KB2630458-x86-ENU.exe|  
|32비트 버전 [Microsoft SQL Server 2008 R2 RTM 기능 팩](http://www.microsoft.com/download/en/details.aspx?id=16978)의 도구 하나 이상|32비트 버전의 Microsoft SQL Server 2008 R2 SP2 Feature Pack으로 도구 업그레이드|[Microsoft SQL Server 2008 R2 SP2 기능 팩](http://go.microsoft.com/fwlink/?LinkId=251792)의 파일 하나 이상|  
|SQL Server 2008 R2의 32비트 설치 없음|Server 2008 R2(SP2 포함) 설치|[SQL Server 2008 R2 SP2 – Express Edition](http://go.microsoft.com/fwlink/?LinkId=251791) 으로 이동하여 지침을 따릅니다.|  
|SQL Server 2008 R2 Management Studio의 32비트 설치 없음|SQL Server 2008 R2 Management Studio(SP2 포함) 설치|[여기](http://go.microsoft.com/fwlink/p/?LinkId=251791) 에 있는 SQLManagementStudio_x86_ENU.exe를 다운로드하여 무료로 SQL Server 2008 R2 SP2 Management Studio Express Edition을 설치합니다.|  
|64비트 버전 SQL Server 2008 R2 또는 SQL Server 2008 R2 SP1의 모든 버전|64비트 버전의 SQL Server 2008 R2 SP2로 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkId=251790)에 있는 SQLServer2008R2SP2-KB2630458-x64-ENU 또는 SQLServer2008R2SP2-KB2630455-IA64-ENU.exe|  
|64비트 버전의 SQL Server 2008 R2 RTM Express 또는 SQL Server 2008 R2 SP1 Express|64비트 버전의 SQL Server 2008 R2 SP2로 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkId=251790)에 있는 SQLServer2008R2SP2-KB2630458-x64-ENU.exe 또는 SQLServer2008R2SP2-KB2630455-IA64-ENU.exe|  
|64비트 버전의 SQL Server 2008 R2 또는 SQL Server 2008 R2 SP1 클라이언트 및 관리 도구(SQL Server 2008 R2 Management Studio 포함)|64비트 버전의 SQL Server 2008 R2 SP2로 클라이언트 및 관리 도구 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkId=251790)에 있는 SQLServer2008R2SP2-KB2630458-x64-ENU.exe 또는 SQLServer2008R2SP2-KB2630455-IA64-ENU.exe|  
|64비트 버전의 SQL Server 2008 R2 Management Studio Express 또는 SQL Server 2008 R2 SP1 Management Studio Express|64비트 버전의 SQL Server 2008 R2 SP2 Management Studio Express로 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkId=251791)에 있는 SQLManagementStudio_x64_ENU.exe|  
|64비트 버전 SQL Server 2008 R2 또는 SQL Server 2008 R2 SP1의 모든 버전 **및** 64비트 버전의 클라이언트 및 관리 도구(SQL Server 2008 R2 RTM Management Studio 포함)|64비트 버전의 SQL Server 2008 R2 SP2로 모든 제품 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkId=251790)에 있는 SQLServer2008R2SP2-KB2630458-x64-ENU.exe|  
|64비트 버전 [Microsoft SQL Server 2008 R2 RTM 기능 팩](http://www.microsoft.com/download/en/details.aspx?id=16978)의 도구 하나 이상|64비트 버전의 Microsoft SQL Server 2008 R2 SP2 기능 팩으로 도구 업그레이드|[Microsoft SQL Server 2008 R2 SP2 기능 팩](http://go.microsoft.com/fwlink/?LinkId=251792)의 파일 하나 이상|  
|SQL Server 2008 R2의 64비트 설치 안 됨|Server 2008 R2(SP2 포함) 설치|[SQL Server 2008 R2 SP2 – Express Edition](http://go.microsoft.com/fwlink/?LinkId=251791) 으로 이동하여 지침을 따릅니다.|  
|SQL Server 2008 R2 Management Studio의 64비트 설치 안 됨|SQL Server 2008 R2 Management Studio(SP2 포함) 설치|[여기](http://go.microsoft.com/fwlink/p/?LinkId=251791) 에 있는 SQLManagementStudio_x64_ENU.exe를 다운로드하여 무료로 SQL Server 2008 R2 SP2 Management Studio Express Edition을 설치합니다.|  
  
### <a name="22-setup-might-fail-if-sqagtresdll-is-locked-by-another-process"></a>2.2 SQAGTRES.dll이 다른 프로세스에 의해 잠겨 있는 경우 설치 실패  
**문제:** 다음 오류로 SQL Server 설치 작업이 실패할 수 있습니다. `Upgrading of cluster resource C:\Program Files\Microsoft SQL Server\MSSQL10_50.<Instance name>\MSSQL\Binn\SQAGTRES.DLL on machine <Computer name> failed with Win32Exception. Please look at inner exception for details.` 근본 원인은 C:\Windows\system32\SQAGTRES.DLL이 다른 프로세스에 의해 잠겨 있고 설치 프로그램에서 업데이트할 수 없었기 때문입니다.  
  
**해결 방법**: C:\Windows\system32\SQAGTRES.DLL의 이름을 C:\Windows\system32\SQAGTRES_old.DLL과 같은 임시 이름으로 바꾼 다음 설치 오류 메시지에서 다시 시도 옵션을 선택합니다. 이렇게 하면 설치를 계속할 수 있습니다. 다시 부팅한 이후에 임시 파일 C:\Windows\system32\SQAGTRES_old.DLL을 삭제하면 됩니다.  
  
## <a name="30-known-issues-fixed-in-this-service-pack"></a>3.0 이 서비스 팩에서 해결된 알려진 문제  
이 서비스 팩에서 해결된 전체 버그 및 알려진 문제 목록은 이 [마스터 KB 문서](http://support.microsoft.com/kb/2630455)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
[SQL  Server  버전 및 에디션 확인 방법](http://support.microsoft.com/kb/321185)  
  
