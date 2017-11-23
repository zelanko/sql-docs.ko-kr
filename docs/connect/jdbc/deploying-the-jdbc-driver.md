---
title: "JDBC 드라이버 배포 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3ad3508d-d9b1-47fb-a63b-21cdc3ed44e0
caps.latest.revision: "26"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: fdeed91effe8c6619121f6ed392237f710a785d8
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="deploying-the-jdbc-driver"></a>JDBC 드라이버 배포
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  에 의존 하는 응용 프로그램을 배포 하는 경우는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], 해당 응용 프로그램과 함께 JDBC driver를 재배포 해야 합니다. Windows Data Access Components (Windows DAC)는 Windows 운영 체제의 구성 요소와 달리 JDBC 드라이버의 구성 요소를 것으로 간주 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
 응용 프로그램과 함께 JDBC 드라이버를 배포하는 데에는 두 가지 접근 방식이 있습니다. 그 중 하나는 JDBC 드라이버 파일을 자체 사용자 지정 설치 패키지의 일부로 포함시키는 것입니다. 두 번째 방법은 아니지만 Microsoft에서 다운로드할 수 있는에서 제공 하는 JDBC 설치 패키지를 사용 하 여 [Microsoft JDBC Driver for SQL Server 개발자 센터](http://go.microsoft.com/fwlink/?LinkId=70166)합니다.  
  
 다음 섹션에서는 Windows 및 UNIX 운영 체제에서 JDBC 설치 패키지를 사용하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  일반적으로 Java 응용 프로그램을 배포하는 방법은 Java 웹 사이트(영문)를 참조하십시오.  
  
## <a name="deploying-the-jdbc-driver-on-windows-systems"></a>Windows 시스템에서 JDBC 드라이버 배포  
 일반적으로 이름이 인 설치 패키지의 zip 실행 파일 버전을 사용 해야 Windows 운영 체제에서 JDBC 드라이버를 배포 하면 `sqljdbc_<version>_<language>.exe`합니다.  
  
 사용 해야 zip 실행 파일을 자동으로 실행 하려면는 `/auto` 명령줄에서 또는 다음과 같이 배치 파일에서 명령줄 옵션:  
  
 `sqljdbc_<version>_<language>.exe /auto`  
  
> [!NOTE]  
>  사용 하는 경우는 `/auto` 하더라도 WinZip 대화 상자가 사용자의 화면에 표시 된 대로 자동 설치는 옵션입니다. 그러나 대화 상자에 답할 필요는 없으며 압축 풀기 작업이 완료되자마자 대화 상자가 닫힙니다.  
  
## <a name="deploying-the-driver-on-unix-systems"></a>UNIX 시스템에서 JDBC 드라이버 배포  
 일반적으로 이름이 인 설치 패키지의 gzip 파일 버전을 사용 해야 UNIX 운영 체제에서 JDBC 드라이버를 배포 하면 `sqljdbc_<version>_<language>.tar.gz`합니다.  
  
 JDBC 드라이버를 설치하기 전에 gzip 및 tar 유틸리티가 모두 사용자 시스템에 설치되어 있으며 이 두 유틸리티에 대한 실행 파일이 들어 있는 폴더가 PATH 환경 변수에 추가되어 있는지 확인해야 합니다.  
  
 압축된 tar 파일의 압축을 풀려면 드라이버의 압축을 풀 디렉터리로 이동하여 다음 명령을 입력합니다.  
  
 `gzip -d sqljdbc_<version>_<language>.tar.gz`  
  
 압축된 tar 파일의 압축을 풀려면 드라이버를 설치할 디렉터리로 파일을 이동하고 다음 명령을 입력합니다.  
  
 `tar –xf sqljdbc_<version>_<language>.tar`  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
