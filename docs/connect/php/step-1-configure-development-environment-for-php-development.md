---
title: '1단계: PHP를 위한 환경 구성'
description: 이 시작 가이드의 1단계에는 PHP 및 Microsoft ODBC Driver for SQL Server를 설치하고 개발 환경을 구성하는 작업이 포함됩니다.
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 0bce6022-00bd-45c6-9671-eaa9dfa395a8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 88eb2c2c67eac3ecd9fba2c79c143de28cf60d22
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81633174"
---
# <a name="step-1-configure-environment-for-php-development"></a>1단계: PHP 개발을 위한 환경 구성
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]




* 여기에 나와 있는 대로 환경에 따라 사용할 PHP 드라이버 버전을 확인합니다.  [Microsoft Drivers for PHP for SQL Server에 대한 시스템 요구 사항](system-requirements-for-the-php-sql-driver.md)
* 해당하는 PHP 드라이버를 다운로드하여 설치할 수 있는 곳: [Microsoft PHP 드라이버 다운로드](https://www.microsoft.com/download/details.aspx?id=20098)  
* 해당하는 ODBC 드라이버를 다운로드하여 설치할 수 있는 곳:  [SQL Server용 ODBC 드라이버 다운로드](../odbc/download-odbc-driver-for-sql-server.md)  
* 다음과 같이 특정 운영 체제에 맞게 PHP 드라이버와 웹 서버를 구성합니다.

### <a name="windows"></a>Windows  
  

* 여기에 나와 있는 대로 PHP 드라이버 로드를 구성합니다. [Microsoft Drivers for PHP for SQL Server 로드](../../connect/php/loading-the-php-sql-driver.md) 
* 여기에 나와 있는 대로 PHP 애플리케이션을 호스팅하도록 IIS를 구성합니다. [Microsoft Drivers for PHP for SQL Server에 대한 IIS 구성](../../connect/php/configuring-iis-for-php-sql-driver.md)

### <a name="linux-and-macos"></a>Linux 및 macOS


*   PHP 드라이버 로드를 구성하고 여기에 나와 있는 대로 PHP 애플리케이션을 호스팅하도록 웹 서버를 구성합니다. [PHP Linux 및 macOS 드라이버 설치 자습서](../../connect/php/installation-tutorial-linux-mac.md)
