---
title: MSSQL_ENG014114 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014114 error
ms.assetid: f5f04590-e1c6-40d8-ab2b-98c791a0fc44
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 51b62a64ae008e0994054d40344d1e0d68bb296b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63191678"
---
# <a name="mssqleng014114"></a>MSSQL_ENG014114
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|14114|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|'%s'이(가) 배포자로 구성되지 않았습니다.|  
  
## <a name="explanation"></a>설명  
 오류 메시지가 'Null'이 아닌 특정 인스턴스를 지정하는 경우 이 지정된 인스턴스는 배포자로 인식되도록 올바르게 구성되지 않은 것입니다.  
  
 메시지가 'Null'을 배포자로 지정하는 경우에는 **master** 데이터베이스에 로컬 서버에 대한 항목이 없거나 컴퓨터 이름이 바뀌어 항목이 정확하지 않은 것입니다. 복제 시 컴퓨터 이름과 인스턴스 이름(옵션)을 사용하여 토폴로지의 모든 서버를 등록해야 하며 클러스터형 인스턴스의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가상 서버 이름과 인스턴스 이름(옵션)이 사용됩니다. 복제가 제대로 수행되려면 토폴로지의 각 서버에 대해 `SELECT @@SERVERNAME` 이 반환한 값이 컴퓨터 이름이나 가상 서버 이름 및 인스턴스 이름(옵션)과 일치해야 합니다.  
  
 IP 주소나 FQDN(정규화된 도메인 이름)으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 등록한 경우에는 복제가 지원되지 않습니다. 복제 구성 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 IP 주소 또는 FQDN으로 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 인스턴스를 등록한 경우 이 오류가 발생할 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 오류 메시지가 특정 인스턴스를 지정하면 서버를 배포자로 구성하십시오. 자세한 내용은 [배포 구성](configure-distribution.md)을 참조하세요.  
  
 메시지가 특정 인스턴스를 지정하지 않으면('Null') 배포자 인스턴스가 적절하게 등록되었는지 확인하십시오. 컴퓨터의 네트워크 이름과 SQL Server 인스턴스의 이름이 다른 경우 다음 중 하나를 수행하십시오.  
  
-   SQL Server 인스턴스 이름을 유효한 네트워크 이름으로 추가합니다. 대체 네트워크 이름을 설정하는 한 가지 방법은 해당 이름을 로컬 호스트 파일에 추가하는 것입니다. 로컬 호스트 파일은 기본적으로 WINDOWS\system32\drivers\etc 또는 WINNT\system32\drivers\etc에 있습니다. 자세한 내용은 Windows 설명서를 참조하십시오.  
  
     예를 들어 컴퓨터 이름이 comp1이고 컴퓨터의 IP 주소가 10.193.17.129이고 인스턴스 이름이 inst1/instname이면 호스트 파일에 다음 항목을 추가하십시오.  
  
     10.193.17.129 inst1  
  
-   배포를 해제하고 인스턴스를 등록한 후 배포를 다시 설정합니다. 비클러스터형 인스턴스에 대해 @@SERVERNAME 값이 올바르지 않으면 다음 단계를 수행하세요.  
  
    ```  
    sp_dropserver '<old_name>', 'droplogins'  
    go  
    sp_addserver '<new_name>', 'local'  
    go  
    ```  
  
     [sp_addserver&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql) 저장 프로시저를 실행한 후에 @@SERVERNAME 변경 내용을 적용하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 다시 시작해야 합니다.  
  
     클러스터형 인스턴스에 대해 @@SERVERNAME 값이 올바르지 않으면 클러스터 관리자를 사용하여 해당 이름을 변경해야 합니다. 자세한 내용은 [Always On 장애 조치(failover) 클러스터 인스턴스(SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](errors-and-events-reference-replication.md)  
  
  
