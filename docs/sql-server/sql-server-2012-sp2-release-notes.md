---
title: "SQL Server 2012 SP2 릴리스 정보 | Microsoft 문서"
ms.prod: sql-server
ms.prod_service: sql-non-specified
ms.service: server-general
ms.component: 
ms.technology: server-general
ms.custom: 
ms.date: 01/31/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 67cb8b3e-3d82-47f4-840d-0f12a3bff565
caps.latest.revision: "6"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 83969d05f234dc5e6384754971ca6eb5a2621006
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sql-server-2012-sp2-release-notes"></a>SQL Server 2012 SP2 Release Notes
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)] 본 릴리스 정보는 SQL Server 2012 서비스 팩 2를 설치하거나 문제를 해결하기 전에 알아두어야 할 문제를 설명합니다. 릴리스 정보는 설치 미디어가 아닌 온라인으로만 제공됩니다. 릴리스 정보는 문제가 발견될 때마다 정기적으로 업데이트됩니다. 자세한 내용은 [SQL Server 2012 서비스 팩 2에서 수정된 버그](http://support.microsoft.com/KB/2958429) 를 참조하세요.  
  
## <a name="choose-the-correct-file-to-download-and-install"></a>다운로드 및 설치할 올바른 파일 선택  
아래 표에서 현재 설치된 버전에 따라 다운로드할 파일의 위치와 이름을 확인하세요. 다운로드 페이지에 시스템 요구 사항 및 기본 설치 지침이 나와 있습니다.  
  
||||  
|-|-|-|  
|**현재 설치된 버전**|**원하는 작업**|**다운로드 및 설치할 파일**|  
|32비트 설치:|||  
|32비트 버전의 SQL  Server  2012|32비트 버전의 SQL Server 2012 SP2로 업그레이드|**SQL Server 2012 SP2 다운로드 페이지**<arch>**-**<lang id>**에 있는** SQLServer2012SP2-KB2958429- [.exe](http://go.microsoft.com/fwlink/?LinkID=401006)|  
|32비트 버전의 SQL  Server  2012  RTM  Express|32비트 버전의 SQL Server 2012 Express SP2으로 업그레이드|**SQL Server 2012 SP2 Express 다운로드 페이지**<arch>**에 있는**<lang>**SQLEXPR_** _ [.msi](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|32비트 버전의 SQL  Server  2012  클라이언트 및 관리 도구(SQL  Server  2012  Management  Studio  포함)|32비트 버전의 SQL Server 2012 SP2로 클라이언트 및 관리 도구 업그레이드|**SQL Server 2012 SP2 Express 다운로드 페이지**<arch>**에 있는**<lang>**SQLEXPRWT_** _ [.msi](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|32비트 버전의 SQL  Server  2012  Management  Studio  Express|32비트 버전의 SQL Server 2012 SP2 Management Studio Express로 업그레이드|**SQL Server 2012 SP2 Express 다운로드 페이지**<arch>**에 있는**<lang>**SQLManagementStudio_** _ [.msi](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|32비트 버전의 SQL Server 2012 및 32비트 버전의 클라이언트 및 관리 도구(SQL Server 2012 RTM Management Studio 포함)|32비트 버전의 SQL Server 2012 SP2로 모든 제품 업그레이드|**SQL Server 2012 SP2 Express 다운로드 페이지**<arch>**에 있는**<lang>**SQLEXPRADV_** _ [.msi](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|[Microsoft SQL Server 2012 RTM 기능 팩](http://www.microsoft.com/download/details.aspx?id=29065) 또는 [Microsoft SQL Server 2012 SP1 기능 팩](http://go.microsoft.com/fwlink/p/?LinkID=268266)에 있는 32비트 버전 도구 하나 이상|32비트 버전의 Microsoft SQL Server 2012 SP2 Feature Pack으로 도구 업그레이드|Microsoft [SQL Server 2012 SP2 기능 팩 다운로드 페이지](http://go.microsoft.com/fwlink/?LinkID=401008)에 있는 도구 하나 이상|  
|64비트 설치:|||  
|64비트 버전의 SQL Server 2012|64비트 버전의 SQL Server 2012 SP2로 업그레이드|<arch>-<langid>SQL Server 2012 SP2 다운로드 페이지 [에 있는 SQLServer2012SP2-KB2958429-](http://go.microsoft.com/fwlink/?LinkID=401006).exe|  
|64비트 버전의 SQL Server 2012 RTM Express|64비트 버전의 SQL Server 2012 SP2로 업그레이드|**SQL Server 2012 SP2 Express 다운로드 페이지**<arch>**에 있는**<lang>**SQLEXPR_** _ [.msi](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|64비트 버전의 SQL Server 2012 클라이언트 및 관리 효율성 도구(SQL Server 2012 Management Studio 포함)|64비트 버전의 SQL Server 2012 SP2로 클라이언트 및 관리 효율성 도구 업그레이드|**SQL Server 2012 SP2 Express 다운로드 페이지**<arch>**에 있는**<lang>**SQLEXPRWT_** _ [.msi](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|64비트 버전의 SQL Server 2012 Management Studio Express|64비트 버전의 SQL Server 2012 SP2 Management Studio Express로 업그레이드|**SQL Server 2012 SP2 Express 다운로드 페이지**<arch>**에 있는**<lang>**SQLManagementStudio_** _ [.msi](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|[Microsoft SQL Server 2012 RTM 기능 팩](http://www.microsoft.com/download/details.aspx?id=29065) 또는 [Microsoft SQL Server 2012 SP1 기능 팩](http://go.microsoft.com/fwlink/p/?LinkID=268266)에 있는 64비트 버전 도구 하나 이상|64비트 버전의 Microsoft SQL Server 2012 SP2 Feature Pack으로 도구 업그레이드|Microsoft [SQL Server 2012 SP2 기능 팩 다운로드 페이지](http://go.microsoft.com/fwlink/?LinkID=401008)에 있는 도구 하나 이상|  
  
