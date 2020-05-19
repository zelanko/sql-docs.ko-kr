---
title: 실행 시 데이터 및 Text, ntext 또는 Image 열 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- data-at-execution
- ODBC data-at-execution
- image columns [ODBC]
ms.assetid: 67ffb1a6-f38d-4712-ba64-96bdd41ec2b2
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4368104ffcad31a59bfa1a3acffb38fcd015156e
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718851"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>실행 시 데이터 및 text, ntext 또는 image 열
  ODBC 실행 시 데이터는 애플리케이션에서 바인딩된 열 또는 매개 변수에 있는 대량의 데이터를 사용할 수 있도록 하는 기능입니다. 매우 큰 **text**, **ntext**또는 **image** 열을 검색할 때 응용 프로그램은 단순히 큰 버퍼를 할당 하 고, 열을 버퍼에 바인딩하고, 행을 인출 하지 못할 수 있습니다. 매우 큰 **text**, **ntext**또는 **image** 열을 업데이트할 때 응용 프로그램은 단순히 큰 버퍼를 할당 하 고 SQL 문에서 매개 변수 표식에 바인딩한 다음 문을 실행 하지 못할 수 있습니다. 이러한 경우 응용 프로그램은 실행 시 데이터 옵션과 함께 [SQLGetData](../native-client-odbc-api/sqlgetdata.md) 또는 [sqlputdata](../native-client-odbc-api/sqlputdata.md) 를 사용 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [text 및 image 열 관리](managing-text-and-image-columns.md)  
  
  
