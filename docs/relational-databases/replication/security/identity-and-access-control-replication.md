---
description: ID 및 Access Control(복제)
title: ID 및 액세스 제어(복제) | Microsoft 문서
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- access controls [SQL Server replication]
- security [SQL Server replication], identity and access control
- authentication [SQL Server replication]
- identity [Replication]
ms.assetid: 4da0e793-1ee4-4f69-a80b-45c6732a238d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 8737fa7c4781110c4a9169a7334e88f7df734291
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479764"
---
# <a name="identity-and-access-control-replication"></a>ID 및 Access Control(복제)
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  인증은 한 엔터티(이 컨텍스트에서는 일반적으로 컴퓨터)가 *보안 주체* 라고도 하는 다른 엔터티(일반적으로 다른 컴퓨터 또는 사용자)의 신원 또는 실체를 확인하는 프로세스입니다. 권한 부여는 파일 시스템의 파일이나 데이터베이스의 테이블과 같은 리소스에 대한 액세스 권한을 인증된 보안 주체에게 부여하는 프로세스입니다.  
  
 복제 보안은 인증 및 권한 부여를 사용하여 복제된 데이터베이스 개체 및 복제 처리와 관련된 컴퓨터와 에이전트에 대한 액세스를 제어합니다. 이 작업은 다음과 같은 3가지 메커니즘을 통해 수행됩니다.  
  
-   에이전트 보안  
  
     복제 에이전트 보안 모델을 사용하여 복제 에이전트를 실행 및 연결하는 계정을 더욱 세밀하게 제어할 수 있습니다. 에이전트 보안 모델에 대한 자세한 내용은 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하십시오. 
  
-   관리 역할  
  
     복제 설정, 유지 관리 및 처리에 올바른 서버 및 데이터베이스 역할이 사용되도록 합니다. 자세한 내용은 [Security Role Requirements for Replication](../../../relational-databases/replication/security/security-role-requirements-for-replication.md)을(를) 참조하세요.  
  
-   PAL(게시 액세스 목록)  
  
     PAL을 통해 게시에 대한 액세스 권한을 부여합니다. PAL 기능은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 액세스 제어 목록과 유사하게 작동합니다. 구독자가 게시자 또는 배포자에 연결하여 게시에 대한 액세스를 요청하면 에이전트가 전달한 인증 정보가 PAL과 비교됩니다. PAL에 대한 자세한 내용 및 모범 사례는 [게시자 보안 설정](../../../relational-databases/replication/security/secure-the-publisher.md)을 참조하세요.  
  
## <a name="filtering-published-data"></a>게시된 데이터 필터링  
 인증 및 권한 부여를 통해 복제된 데이터 및 개체에 대한 액세스를 제어하는 옵션 외에도 복제에는 구독자에서 사용 가능한 데이터를 제어하는 두 가지 옵션, 즉 열 필터링과 행 필터링이 있습니다. 필터링에 대한 자세한 내용은 [게시된 데이터 필터링](../../../relational-databases/replication/publish/filter-published-data.md)을 참조하세요.  
  
 아티클을 정의할 때는 게시에 필요한 열만 게시하고 불필요하거나 중요한 데이터를 포함하는 열은 생략할 수 있습니다. 예를 들어 Adventure Works 데이터베이스의 **Customer** 테이블을 현장에 있는 영업 담당자에게 게시하는 경우 회사 중역에게만 필요한 **AnnualSales** 열은 생략할 수 있습니다.  
  
 게시된 데이터를 필터링하여 데이터에 대한 액세스를 제한할 수 있고 구독자에서 사용 가능한 데이터를 지정할 수 있습니다. 예를 들어 **Customer** 테이블을 필터링하여 협력사에서는 **ShareInfo** 열의 값이 "예"인 고객에 대한 정보만 받도록 할 수 있습니다. 병합 복제에서 HOST_NAME()을 포함하는 매개 변수가 있는 필터를 사용할 경우 보안 고려 사항이 있습니다. 자세한 내용은 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)의 "HOST_NAME()으로 필터링" 섹션을 참조하십시오.  

## <a name="manage-logins-and-passwords-in-replication"></a>복제의 로그인 및 암호 관리
복제를 구성할 때 복제 에이전트에 대한 로그인과 암호를 지정합니다. 복제를 구성한 후에는 로그인과 암호를 변경할 수 있습니다. 자세한 내용은 [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)을(를) 참조하세요. 복제 에이전트에서 사용하는 계정의 암호를 변경하는 경우 [sp_changereplicationserverpasswords&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql.md)를 실행합니다.  

gMSA(그룹 관리 서비스 계정)의 사용에 대한 지원은 SQL Server 2014에 도입되었습니다. 자세한 내용은 [복제 및 그룹 관리 서비스 계정](https://repltalk.com/2019/03/26/replication-and-group-managed-service-accounts/) 블로그를 참조하세요.
  
## <a name="see-also"></a>참고 항목  
 [위협 요소 및 취약성 완화&#40;복제&#41;](../../../relational-databases/replication/security/threat-and-vulnerability-mitigation-replication.md) [복제 에이전트 보안 모델](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [복제 보안을 위한 최선의 구현 방법](../../../relational-databases/replication/security/replication-security-best-practices.md)   

  
  
