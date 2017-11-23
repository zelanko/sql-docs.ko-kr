---
title: "RemoveCertificate 메서드 (ServerSettings 클래스) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: RemoveCertificate Method (ServerSettings Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: RemoveCertificate method
ms.assetid: 9ffdbc39-93f5-48fb-859a-86a3ad545827
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fa3f1f89cb8f4259c5a2c250c63b6a5eb3814fbe
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="removecertificate-method-serversettings-class"></a>RemoveCertificate 메서드(ServerSettings 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]인스턴스에서 현재 보안 인증서를 제거 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.RemoveCertificate()  
```  
  
## <a name="parts"></a>부분  
 *개체*  
 [인스턴스의 서버 설정을 나타내는](../../../relational-databases/wmi-provider-configuration-classes/serversettings-class/serversettings-class.md) ServerSettings 클래스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 u**int32** 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>주의  
  
## <a name="see-also"></a>관련 항목:  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
