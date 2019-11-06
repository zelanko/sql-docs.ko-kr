---
title: JDBC 드라이버 배포 | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3ad3508d-d9b1-47fb-a63b-21cdc3ed44e0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 518f6bd2605d92857520f870b20edcd351771c54
ms.sourcegitcommit: 4fb6bc7c81a692a2df706df063d36afad42816af
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2019
ms.locfileid: "73049842"
---
# <a name="deploying-the-jdbc-driver"></a>JDBC 드라이버 배포
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]를 사용하는 애플리케이션을 배포하는 경우 해당 애플리케이션과 함께 JDBC 드라이버도 다시 배포해야 합니다. Windows 운영 체제의 구성 요소인 Windows DAC(Windows Data Access Components)와 달리 JDBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 구성 요소로 간주됩니다.  
  
 애플리케이션과 함께 JDBC 드라이버를 배포하는 데에는 두 가지 접근 방식이 있습니다. 그 중 하나는 JDBC 드라이버 파일을 자체 사용자 지정 설치 패키지의 일부로 포함시키는 것입니다. 나머지 방식은 Microsoft가 제공하는 JDBC 설치 패키지를 사용하는 것인데, 이는 [SQL Server용 Microsoft JDBC 드라이버 개발자 센터](https://go.microsoft.com/fwlink/?LinkId=70166)에서 다운로드할 수 있습니다.  
  
 다음 섹션에서는 Windows 및 UNIX 운영 체제에서 JDBC 설치 패키지를 사용하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  일반적으로 Java 애플리케이션을 배포하는 방법은 Java 웹 사이트(영문)를 참조하십시오.  
  
## <a name="deploying-the-jdbc-driver-on-windows-systems"></a>Windows 시스템에서 JDBC 드라이버 배포  
 Windows 운영 체제에서 JDBC 드라이버를 배포하는 경우 일반적으로 이름이 `sqljdbc_<version>_<language>.exe`인 설치 패키지의 zip 실행 파일 버전을 사용해야 합니다.  
  
 이 zip 실행 파일을 자동으로 실행하려면 다음과 같이 명령줄이나 배치 파일에서 `/auto` 명령줄 옵션을 사용해야 합니다.  
  
 `sqljdbc_<version>_<language>.exe /auto`  
  
> [!NOTE]  
>  `/auto` 옵션을 사용하더라도 WinZip 대화 상자가 사용자 화면에 표시되므로 완전한 자동 설치 작업은 아닙니다. 그러나 대화 상자에 답할 필요는 없으며 압축 풀기 작업이 완료되자마자 대화 상자가 닫힙니다.  
  
## <a name="deploying-the-driver-on-unix-systems"></a>UNIX 시스템에서 JDBC 드라이버 배포 
 UNIX 운영 체제에서 JDBC 드라이버를 배포하는 경우 일반적으로 이름이 `sqljdbc_<version>_<language>.tar.gz`인 설치 패키지의 gzip 파일 버전을 사용해야 합니다.  
  
 JDBC 드라이버를 설치하기 전에 gzip 및 tar 유틸리티가 모두 사용자 시스템에 설치되어 있으며 이 두 유틸리티에 대한 실행 파일이 들어 있는 폴더가 PATH 환경 변수에 추가되어 있는지 확인해야 합니다.  
  
 압축된 tar 파일의 압축을 풀려면 드라이버의 압축을 풀 디렉터리로 이동하여 다음 명령을 입력합니다.  
  
 `gzip -d sqljdbc_<version>_<language>.tar.gz`  
  
 압축된 tar 파일의 압축을 풀려면 드라이버를 설치할 디렉터리로 파일을 이동하고 다음 명령을 입력합니다.  
  
 `tar -xf sqljdbc_<version>_<language>.tar`  

## <a name="legalities-of-driver-redistribution"></a>Legalities 드라이버 재배포

JDBC 드라이버 버전 6.0, 6.2, 6.4 및 7.0은 재배포 가능 합니다. 라이선스 계약의 _배포 가능 코드_ 절을 검토하세요.

JDBC 드라이버 버전 4.x는 오래 된 버전입니다. 2018에 대 한 지원이 만료 되었습니다.

## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
