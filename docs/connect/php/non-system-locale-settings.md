---
title: 비시스템 로캘 설정 | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- locale, linux, macOS, system
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: bd60bff3ab9ee19b1a1d2435e69651ea054689e7
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "76913326"
---
# <a name="non-system-locale-settings"></a>비시스템 로캘 설정
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 섹션은 Linux 및 macOS 사용자에게만 적용됩니다. 특히 php 애플리케이션에서 둘 이상의 로캘을 처리하는 사용자에 해당합니다.

기본적으로 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]는 시스템에 정의된 `LC_ALL` 환경 변수를 사용하고 다른 모든 `LC_xxx` 범주(경우에 따라 `$LANG` 또는 `$LANGUAGE`를 제외)를 재정의하여 천 단위 구분 기호, 소수점 문자, 문자 집합, 월, 요일 이름, 애플리케이션 메시지(예: 오류 메시지), 통화 기호 등에 영향을 줍니다.

버전 5.8.0부터 사용자는 아래 예제와 같이 php.ini 파일을 사용하여 지역화 설정을 구성할 수 있습니다.

## <a name="set-locale-info-using-the-sqlsrv-driver"></a>SQLSRV 드라이버를 사용하여 로캘 정보 설정  
php.ini 파일의 끝에 다음을 추가합니다.
  
```  
[sqlsrv]  
sqlsrv.SetLocaleInfo = <option>
```  
  
## <a name="set-locale-info-using-the-pdo_sqlsrv-driver"></a>PDO_SQLSRV 드라이버를 사용하여 로캘 정보 설정  
php.ini 파일의 끝에 다음을 추가합니다.
  
```  
[pdo_sqlsrv]  
pdo_sqlsrv.set_locale_info = <option>
```  
  
**옵션**은 다음 중 하나가 될 수 있습니다.  
  
|옵션|동작 설명|
|---------|---------------|
|0|드라이버가 시스템 로캘 설정을 무시합니다.|
|1|드라이버가 LC_CTYPE 변수를 읽습니다.|
|2|드라이버가 LC_ALL 변수를 읽습니다(기본값).|
  

`LC_CTYPE` 범주는 문자 처리 규칙을 결정합니다. 이 규칙은 텍스트 데이터 문자의 바이트 시퀀스, 문자 분류 및 문자 클래스 동작에 대한 해석을 제어합니다. 대문자 및 소문자, 영문자 및 영문자 이외 문자에 대한 인식을 제어합니다.

### <a name="explanation"></a>설명

1. 옵션 0 -- 애플리케이션 로캘을 변경하지 않으려는 경우 이 옵션을 사용합니다.

1. 옵션 1 -- 다른 `LC_CTYPE` 범주에 영향을 주지 않고 `LC_xxx`의 시스템 값만 설정하려면 이 옵션을 사용합니다.

1. 옵션 2 -- `LC_ALL`을 사용하여 모든 `LC_xxx` 범주를 재정의합니다(php 애플리케이션 및 해당 확장에 영향을 미침).

php 스크립트의 로캘이 시스템 로캘과 동일하지 않은 경우에는 php 기본 제공 함수인 [setlocale](https://www.php.net/manual/en/function.setlocale.php)을 호출하여 php 스크립트에서 로캘을 지정해야 할 수 있습니다. 

예를 들어 시스템 기본값이 `en_US.UTF-8`이지만 php 스크립트에서 `de_DE.UTF-8`을 사용하는 경우 php 함수 `setlocale()`를 적절히 호출합니다.

옵션 2의 경우 `LC_ALL` 변수와 다른 경우에만 php 스크립트에서 원하는 로캘을 지정합니다.

> [!NOTE]
> php에 아무 것도 정의되지 않은 경우 현재 기본값은 `LC_ALL`을 기반으로 하는 다른 모든 로캘 설정을 재정의하는 것입니다. 이 설정은 더 이상 **사용되지 않습니다**. 가까운 장래에 기본값은 시스템 로캘 설정을 무시하는 것입니다. 따라서 사용자가 현재 동작을 유지하려는 경우에는 php.ini 파일을 적절히 수정해야 합니다.

sqlsrv 및 pdo_sqlsrv 드라이버를 모두 사용하는 경우 두 드라이버에 다른 옵션을 설정하는 것은 권장하지 않습니다.