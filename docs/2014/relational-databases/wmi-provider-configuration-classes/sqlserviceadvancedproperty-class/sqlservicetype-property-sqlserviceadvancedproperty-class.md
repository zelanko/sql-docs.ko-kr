---
title: SqlServiceType 속성 (SqlServiceAdvancedProperty 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- SqlServiceType Property (SqlServiceAdvancedProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SqlServiceType property
ms.assetid: 20f1663a-9a14-4f14-8c1b-8aa133e272c3
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 314c7690842ba4f8d54747ef1285b647c3e90a7f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080834"
---
# <a name="sqlservicetype-property-sqlserviceadvancedproperty-class"></a>SqlServiceType 속성(SqlServiceAdvancedProperty 클래스)
  고급 속성과 연결된 관리되는 서비스의 유형을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.SetBoolValue(  
NumValue  
)  
  
```  
  
## <a name="parts"></a>부분  
 *object*  
 고급 속성을 나타내는 [SqlServiceAdvancedProperty 클래스](sqlserviceadvancedproperty-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 유형을 지정하는 uint32 값입니다.  
  
## <a name="remarks"></a>Remarks  
 반환 값은 다음 중 하나일 수 있습니다.  
  
|형식|정의|  
|----------|----------------|  
|*1.*|MSSQLSERVER는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스입니다.|  
|*2*|SQLSERVERAGENT는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 서비스입니다.|  
|*3*|MSFTESQL은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 전체 텍스트 검색 엔진 서비스입니다.|  
|*4*|MsDtsServer는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 서비스입니다.|  
|*5*|MSSQLServerOLAPService는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 서비스입니다.|  
|*6*|ReportServer는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 서비스입니다.|  
|*7*|SQLBrowser는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Browser 서비스입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [서비스 시작 및 중지](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  