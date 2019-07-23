---
title: '1단계: PHP 개발을 위한 개발 환경 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 0bce6022-00bd-45c6-9671-eaa9dfa395a8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc923e3f6e24290f7f2c869fa15dfa4305776452
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68014865"
---
# <a name="step-1-configure-environment-for-php-development"></a>1 단계: PHP 개발을 위한 환경 구성
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]




* 사용자 환경에 따라 사용할 PHP 드라이버 버전을 확인 합니다. 여기에 설명 [된 대로 Microsoft Drivers FOR php for The System 요구 사항에 대 한 시스템 요구 사항 SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)
* 해당 하는 PHP 드라이버를 다운로드 하 여 설치 합니다. [MICROSOFT PHP 드라이버 다운로드](https://www.microsoft.com/download/details.aspx?id=20098)  
* 해당 하는 ODBC 드라이버를 다운로드 하 여 설치 [합니다. SQL Server에 대 한 Odbc 드라이버 다운로드](../../connect/odbc/download-odbc-driver-for-sql-server.md)  
* 특정 운영 체제에 맞게 PHP 드라이버와 웹 서버를 구성 합니다.

### <a name="windows"></a>Windows  
  

* 다음에 설명 된 대로 PHP 드라이버 로드 구성: [php 용 Microsoft 드라이버 로드 SQL Server](../../connect/php/loading-the-php-sql-driver.md) 
* 다음에 설명 된 대로 PHP 응용 프로그램을 호스팅하도록 IIS를 구성 합니다. SQL Server 용 Microsoft driver for PHP에 대 한 [Iis 구성](../../connect/php/configuring-iis-for-php-sql-driver.md)

### <a name="linux-and-mac"></a>Linux 및 Mac


*   Php 드라이버 로드를 구성 하 고 php [Linux 및 Mac 드라이버 설치 자습서](../../connect/php/installation-tutorial-linux-mac.md) 에서 설명한 대로 php 응용 프로그램을 호스팅하도록 웹 서버를 구성 합니다.
