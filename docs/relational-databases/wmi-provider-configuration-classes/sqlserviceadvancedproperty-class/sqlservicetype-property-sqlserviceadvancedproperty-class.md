---
title: SqlServiceType 속성 (SqlServiceAdvancedProperty 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SqlServiceType Property (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServiceType property
ms.assetid: 20f1663a-9a14-4f14-8c1b-8aa133e272c3
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 440d7a0d90887d6a1bbeb9553306c5453c514d02
ms.sourcegitcommit: 20d24654e056561fc33cadc25eca8b4e7f214b1b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67351585"
---
# <a name="sqlservicetype-property-sqlserviceadvancedproperty-class"></a>SqlServiceType 속성(SqlServiceAdvancedProperty 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  고급 속성과 연결된 관리되는 서비스의 유형을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SetBoolValue(NumValue)  
```  
  
## <a name="parts"></a>부분  
 *object*  
 고급 속성을 나타내는 [SqlServiceAdvancedProperty 클래스](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 유형을 지정하는 uint32 값입니다.  
  
## <a name="remarks"></a>Remarks  
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
|*8*|NsService는는 [!INCLUDE[ssNoVersion](../../../includes/ssns-md.md)] 알림 서비스.|  
|*9*|MSSQLFDLauncher 되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 전체 텍스트 필터 데몬 시작 관리자 서비스입니다.|  
|*10*|SQLPBENGINE 되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Polybase 엔진 서비스입니다.|  
|*11*|SQLPBDMS 되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Polybase 데이터 이동 서비스입니다.|  
|*12*|MSSQLLaunchpad 되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 실행 패드 서비스입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [서비스 시작 및 중지](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
