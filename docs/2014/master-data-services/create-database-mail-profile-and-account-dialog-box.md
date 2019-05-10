---
title: 데이터베이스 메일 프로필 및 계정 만들기 대화 상자 (Master Data Services 구성 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.dbmailprofileacct.f1
ms.assetid: b93ea3d4-9f22-490e-8e26-d766b454aed6
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: b614422d3670dc30e0714b18bbf42ed87f1886af
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65483272"
---
# <a name="create-database-mail-profile-and-account-dialog-box-master-data-services-configuration-manager"></a>데이터베이스 메일 프로필 및 계정 만들기 대화 상자(Master Data Services 구성 관리자)
  **데이터베이스 메일 프로필 및 계정 만들기** 대화 상자를 사용하여 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에 대한 데이터베이스 메일 프로필 및 데이터베이스 메일 계정을 만들 수 있습니다. 이 프로필은 비즈니스 규칙 유효성 검사가 실패한 경우 사용자와 그룹에 전자 메일로 알리는 데 사용됩니다.  
  
## <a name="database-mail-profile-and-account"></a>데이터베이스 메일 프로필 및 계정  
 *데이터베이스 메일 프로필* 은 데이터베이스 메일 계정의 모음입니다. *데이터베이스 메일 계정* 에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 전자 메일 메시지를 SMTP 서버로 보내기 위해 사용하는 정보가 포함되어 있습니다. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]에서 프로필 및 계정을 만들면 계정이 프로필에 자동으로 추가되고 해당 계정 정보가 전자 메일을 보내는 데 사용됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 를 사용하여 기존 데이터베이스 메일 프로필 또는 계정을 업데이트하거나 프로필에 대한 계정을 두 개 이상 구성할 수 없습니다. 데이터베이스 메일로 보다 고급 태스크를 수행하려면 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 또는 Transact-SQL 스크립트를 사용할 수 있습니다. 자세한 내용은 SQL Server 온라인 설명서의 [Database Mail Configuration Objects](../relational-databases/database-mail/database-mail-configuration-objects.md) 섹션을 참조하십시오.  
  
|컨트롤 이름|Description|  
|------------------|-----------------|  
|**프로필 이름**|새 데이터베이스 메일 프로필의 이름을 입력합니다. 이 이름은 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에 대해 구성된 데이터베이스 메일 프로필 간에 고유해야 합니다.<br /><br /> 이 프로필을 만든 후에는 **의** 데이터베이스 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]페이지에서 프로필을 선택하고 사용할 수 있습니다.|  
|**계정 이름**|이 프로필과 연결할 새 데이터베이스 메일 계정의 이름을 입력합니다. 이 이름은 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에 대해 구성된 데이터베이스 메일 계정 간에 고유해야 합니다. 이 계정은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 계정 및 Windows 사용자 계정에 해당되지 않습니다.|  
  
## <a name="outgoing-smtp-mail-server"></a>보내는(SMTP) 메일 서버  
  
|컨트롤 이름|Description|  
|------------------|-----------------|  
|**전자 메일 주소**|계정에 대한 전자 메일 주소의 이름을 입력합니다. 이 주소는 메일을 보내는 메일 주소이며 *email_name*@*domain_name* 이메일 주소의 예는 sales@contoso.com입니다.|  
|**표시 이름**|선택적 설정입니다. 이 계정을 사용하여 보낼 전자 메일 메시지에 표시할 이름(예: Contoso Sales Group)을 입력합니다.|  
|**회신 전자 메일 주소**|선택적 설정입니다. 이 계정에서 보낸 전자 메일 메시지에 대한 회신에 사용할 전자 메일 회신 이메일 주소의 예는 admin@contoso.com입니다.|  
|**SMTP 서버**|계정에서 전자 메일을 보내기 위해 사용하는 SMTP 서버의 이름 또는 IP 주소를 입력합니다. 서버 형식 예 SMTP `smtp.` *< company_name >*`.com`합니다. 이에 대한 도움을 얻으려면 메일 관리자에게 문의하십시오.|  
|**포트 번호**|이 계정에 대한 SMTP 서버의 포트 번호를 입력합니다. 기본 SMTP 포트는 25입니다.|  
|**이 서버에는 보안 연결(SSL)이 필요합니다.**|SSL(Secure Sockets Layer)을 사용하여 통신을 암호화합니다.|  
  
## <a name="smtp-authentication"></a>SMTP 인증  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]의 자격 증명 또는 사용자가 제공하는 다른 자격 증명을 사용하거나 익명으로 데이터베이스 메일을 보낼 수 있습니다. 전자 메일 서버에 인증이 필요한 경우 데이터베이스 메일에 사용할 특정 사용자 계정을 만드는 것이 좋습니다. 이 사용자 계정에는 최소한의 권한만 제공하고 다른 용도로 사용하지 말아야 합니다.  
  
|컨트롤 이름|Description|  
|------------------|-----------------|  
|**데이터베이스 엔진 서비스 자격 증명을 사용한 Windows 인증**|데이터베이스 메일에서 SMTP 서버 인증에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] Windows 서비스 계정의 자격 증명을 사용하도록 지정합니다.|  
|**기본 인증**|데이터베이스 메일에서 SMTP 서버 인증에 특정 사용자 이름과 암호를 사용하도록 지정합니다. 이 정보는 전자 메일 서버 인증에만 사용되며 계정이 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 사용자 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 실행하는 컴퓨터의 사용자에 해당할 필요는 없습니다.|  
|**사용자 이름**|데이터베이스 메일에서 SMTP 서버에 로그온하는 데 사용하는 사용자 계정의 이름을 입력합니다. SMTP 서버에 기본 인증이 필요한 경우 사용자 이름은 필수 사항입니다.|  
|**암호**|데이터베이스 메일에서 SMTP 서버에 로그온하는 데 사용하는 암호를 입력합니다. SMTP 서버에 기본 인증이 필요한 경우 암호는 필수 사항입니다.|  
|**암호 확인**|암호를 다시 입력하여 암호를 확인합니다.|  
|**익명 인증**|SMTP 서버에 인증이 필요하지 않음을 지정합니다. 데이터베이스 메일은 SMTP 서버 인증에 자격 증명을 사용하지 않습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 구성 페이지&#40;Master Data Services 구성 관리자&#41;](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [Master Data Services에 대한 데이터베이스 및 웹 사이트 설정](set-up-the-database-and-website-for-master-data-services.md)  
  
  
