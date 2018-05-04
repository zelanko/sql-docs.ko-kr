---
title: SqlServiceType 속성 (SqlServiceAdvancedProperty 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- SqlServiceType Property (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServiceType property
ms.assetid: 20f1663a-9a14-4f14-8c1b-8aa133e272c3
caps.latest.revision: 42
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d752b3879880fccf8eccf86a453afacf466ea7af
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlservicetype-property-sqlserviceadvancedproperty-class"></a>SqlServiceType 속성(SqlServiceAdvancedProperty 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  고급 속성과 연결된 관리되는 서비스의 유형을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SetBoolValue(NumValue)  
```  
  
## <a name="parts"></a>부분  
 *개체*  
 고급 속성을 나타내는 [SqlServiceAdvancedProperty 클래스](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 유형을 지정하는 uint32 값입니다.  
  
## <a name="remarks"></a>주의  
 반환 값은 다음 중 하나일 수 있습니다.  
  
|형식|정의|  
|----------|----------------|  
|*1*|MSSQLSERVER는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스입니다.|  
|*2*|SQLSERVERAGENT는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 서비스입니다.|  
|*3*|MSFTESQL은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 전체 텍스트 검색 엔진 서비스입니다.|  
|*4*|MsDtsServer는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 서비스입니다.|  
|*5*|MSSQLServerOLAPService는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 서비스입니다.|  
|*6*|ReportServer는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 서비스입니다.|  
|*7*|SQLBrowser는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Browser 서비스입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [서비스 시작 및 중지](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
