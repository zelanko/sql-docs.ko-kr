---
title: 로그 파일 뷰어 F1 도움말 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: logs
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- sql13.swb.configurelogs.errorlog.f1
helpviewer_keywords:
- Log File Viewer
ms.assetid: 2243845c-4880-4aa0-9ee8-0a97a128996b
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0600a7c8f64ba6d5b53b8826e53ca1c5371ebdc2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="log-file-viewer-f1-help"></a>로그 파일 뷰어 F1 도움말
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  로그 파일 뷰어는 다양한 구성 요소의 로그 정보를 표시합니다. 로그 파일 뷰어를 연 다음 **로그 선택** 창을 사용하여 표시할 로그를 선택할 수 있습니다. 각 로그는 해당 로그 유형에 적합한 열을 표시합니다.  
  
 사용 가능한 로그는 로그 파일 뷰어를 여는 방법에 따라 다릅니다. 자세한 내용은 [로그 파일 뷰어 열기](../../relational-databases/logs/open-log-file-viewer.md)를 참조하세요.  
  
 감사 로그에 대해 표시되는 행 수는 **도구/옵션** 대화 상자의 **SQL Server 개체 탐색기/명령** 페이지에서 구성할 수 있습니다. 감사 로그에 대해 표시되는 열에 대한 설명은 [sys.fn_get_audit_file&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **로그 로드**  
 로드할 로그 파일을 지정할 수 있는 대화 상자를 엽니다.  
  
 **내보내기**  
 **로그 파일 요약** 표에 표시된 정보를 텍스트 파일로 내보낼 수 있는 대화 상자를 엽니다.  
  
 **새로 고침**  
 선택한 로그의 뷰를 새로 고칩니다. **새로 고침** 단추를 누르면 필터 설정을 적용하는 동안 대상 서버에서 선택한 로그를 다시 읽습니다.  
  
 **필터**  
 **연결**, **날짜**또는 기타 **일반** 필터 조건과 같이 로그 파일 필터링에 사용되는 설정을 지정할 수 있는 대화 상자를 엽니다.  
  
 **검색**  
 로그 파일에서 특정 텍스트를 검색합니다. 와일드카드 문자를 사용한 검색은 지원되지 않습니다.  
  
 **중지**  
 로그 파일 항목의 로드를 중지합니다. 예를 들어 원격 또는 오프라인 로그 파일을 로드하는 데 시간이 오래 걸리며 최근 항목만 보려는 경우 이 옵션을 사용할 수 있습니다.  
  
 **로그 파일 요약**  
 이 정보 창에는 로그 파일 필터링에 대한 요약이 표시됩니다. 파일을 필터링하지 않은 경우 **적용된 필터 없음**이 표시됩니다. 로그에 필터를 적용한 경우에는 **로그 항목 필터링 조건:** \<필터 조건>이 표시됩니다.  
  
 **선택한 행 정보**  
 선택한 이벤트 행에 대한 추가 정보를 페이지 아래쪽에 표시하려면 해당 행을 선택합니다. 열을 표의 새 위치로 끌어서 다시 정렬할 수 있습니다. 표 머리글의 열 구분선을 왼쪽이나 오른쪽으로 끌어 열의 크기를 조정할 수도 있습니다. 열 내용에 맞게 열 너비를 자동 조정하려면 표 머리글의 열 구분선을 두 번 클릭합니다.  
  
 **인스턴스**  
 이벤트가 발생한 인스턴스의 이름입니다. 이 이름은 *컴퓨터 이름*\\*인스턴스 이름*으로 표시됩니다.  
  
## <a name="frequently-displayed-columns"></a>일반적으로 표시되는 열  
 **날짜**  
 이벤트의 날짜를 표시합니다.  
  
 **원본**  
 서비스의 이름(예: MSSQLSERVER)과 같이 이벤트가 생성된 원본 기능을 표시합니다. 이 열은 일부 로그 유형의 경우에만 나타납니다.  
  
 **메시지**  
 이벤트와 관련된 메시지를 표시합니다.  
  
 **로그 유형**  
 이벤트가 속한 로그의 유형을 표시합니다. 선택한 모든 로그가 로그 파일 요약 창에 나타납니다.  
  
 **로그 원본**  
 이벤트가 캡처되는 원본 로그에 대한 설명을 표시합니다.  
  
## <a name="permissions"></a>사용 권한  
 온라인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 로그 파일에 액세스하려면 securityadmin 고정 서버 역할의 멤버 자격이 필요합니다.  
  
 오프라인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 로그 파일에 액세스하려면 **Root\Microsoft\SqlServer\ComputerManagement10** WMI 네임스페이스 및 로그 파일이 저장된 폴더 모두에 대한 읽기 권한이 있어야 합니다. 자세한 내용은 [오프라인 로그 파일 보기](../../relational-databases/logs/view-offline-log-files.md)항목의 보안 섹션을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [로그 파일 뷰어](../../relational-databases/logs/log-file-viewer.md)   
 [로그 파일 뷰어 열기](../../relational-databases/logs/open-log-file-viewer.md)   
 [오프라인 로그 파일 보기](../../relational-databases/logs/view-offline-log-files.md)  
  
  
