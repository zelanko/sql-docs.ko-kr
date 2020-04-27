---
title: DatabaseLogonType 속성(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- DatabaseLogonType
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DatabaseLogonType property
ms.assetid: 6b592582-4c35-4029-ab86-982fff47d8d6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b58c380b85e412554eb47315dfe356d3bff08d03
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66097817"
---
# <a name="databaselogontype-property-wmi-msreportserver_configurationsetting"></a>DatabaseLogonType 속성(WMI MSReportServer_ConfigurationSetting)
  보고서 서버가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 서비스 계정, Windows 사용자 계정 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 사용하여 보고서 서버 데이터베이스에 액세스하는지 여부를 지정합니다. 읽기 전용입니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Dim DatabaseLogonType As Integer  
```  
  
```csharp  
public int DatabaseLogonType;  
```  
  
## <a name="property-values"></a>속성 값  
 로그인 유형을 나타내는 `integer` 개체입니다.  
  
## <a name="example-code"></a>코드 예  
 [MSReportServer_ConfigurationSetting 클래스](msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>설명  
 값은 다음과 같습니다.  
  
-   0: Windows 로그인  
  
-   1: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인  
  
-   2: 서비스로 로그인  
  
 0(Windows)을 지정하는 경우 [DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md) 속성의 값을 해당하는 Windows 사용자 계정으로 설정해야 합니다.  
  
 1(SQL Server)을 지정하는 경우 [DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md) 값이 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이어야 합니다.  
  
 2(Windows 서비스)를 지정하는 경우 보고서 서버는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 계정과 Windows 서비스 계정을 사용하여 보고서 서버 데이터베이스에 액세스합니다. DatabaseLogonAccount 속성은 무시됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  
