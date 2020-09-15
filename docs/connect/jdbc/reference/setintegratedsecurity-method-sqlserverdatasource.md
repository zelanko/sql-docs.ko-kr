---
description: setIntegratedSecurity 메서드(SQLServerDataSource)
title: setIntegratedSecurity 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setIntegratedSecurity
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c968ee4-b041-424a-bf69-cc2c4a4f51c6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b172631e774f5ea9da15873a1e8a00121ab46faf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431855"
---
# <a name="setintegratedsecurity-method-sqlserverdatasource"></a>setIntegratedSecurity 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  integratedSecurity 속성이 사용되는지 여부를 나타내는 **Boolean** 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setIntegratedSecurity(boolean enable)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *enable*  
  
 integratedSecurity가 사용되면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 Windows 자격 증명을 사용하여 애플리케이션 사용자를 인증하도록 하려면 “**true**”로 설정합니다. “**true**”로 설정할 경우 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 로컬 컴퓨터 자격 증명 캐시에서 컴퓨터 또는 네트워크 로그온 시 이미 제공된 자격 증명을 검색합니다. “**false**”로 설정하는 경우 사용자 이름과 암호를 입력해야 합니다.  
  
> [!NOTE]  
>  이 속성은 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] Windows 운영 체제에서만 지원됩니다.  
  
 통합 인증을 사용하는 방법에 대한 자세한 내용은 [연결 URL 빌드](../../../connect/jdbc/building-the-connection-url.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
