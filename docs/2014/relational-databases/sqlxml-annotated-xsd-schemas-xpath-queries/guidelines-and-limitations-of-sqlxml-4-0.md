---
title: 지침 및 SQLXML 4.0의 제한 사항 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, about SQLXML
ms.assetid: fe433d30-90a1-421e-85c6-af13294dc18d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ffe5c84f4ac76fe339735b50843185d122b1cb70
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52806145"
---
# <a name="guidelines-and-limitations-of-sqlxml-40"></a>SQLXML 4.0에 대한 지침 및 제한 사항
  SQLXML 4.0에서 작업을 수행할 때는 다음 사항을 기억해야 합니다.  
  
-   쿼리 결과로 반환되는 XML은 XML을 생성한 매핑 스키마에 대해 유효성이 검사되지 않습니다.  
  
-   SQLXML 4.0에는 버전 독립 및 버전 종속 PROGID가 포함되어 있습니다. 모든 프로덕션 응용 프로그램에는 버전 종속 PROGID를 사용하는 것이 좋습니다. 특히 SQLXML 4.0은 이전 버전과 완벽하게 호환되지 않는다는 점을 감안할 때 이는 매우 중요합니다. 버전 종속 PROGID를 사용하면 새 버전을 설치할 때 발생할 수 있는 프로덕션 오류를 피할 수 있습니다. 버전이 업데이트되면서 버그 픽스, 디자인 변경 등의 다양한 이유로 프로그램 동작이 변경될 수 있습니다. 버전 종속 PROGID를 사용하면 새 버전을 설치할 때 발생할 수 있는 예기치 않은 오류를 피할 수 있습니다. 새 버전을 설치할 때 버전 종속 PROGID를 사용하면 이후에도 응용 프로그램이 오류 없이 정상적으로 작동합니다. 이전 버전 종속 PROGID를 변경하고 새 버전의 최신 버전 종속 PROGID를 사용하려면 프로덕션 환경에 설치하기 전에 응용 프로그램을 테스트해야 합니다. 예를 들어 다음과 같은 시나리오에서 버전 독립 PROGID를 사용하는 응용 프로그램에 문제가 발생할 수 있습니다.  
  
     SQLXML 4.0 및 버전 독립 PROGID를 사용하는 응용 프로그램을 실행하고 있는데 다른 몇 가지 소프트웨어 프로그램을 설치하려는 경우. 해당 프로그램에 의해 이전 버전의 SQLXML이 설치될 수 있습니다. 해당 응용 프로그램의 버전 독립 PROGID가 응용 프로그램에 현재 사용되고 있는 기능이 없을 수도 있는 이전 버전의 SQLXML을 가리키게 되므로 응용 프로그램에 문제가 발생할 수 있습니다.  
  
-   SQLXMLOLEDB 공급자를 사용 하려면 하지을 대신 SQLOLEDB를 사용 하려면 어떤 이유로 공급자를 SQLXML 기능을 설정 합니다 **SQLXML Version** 속성을 "SQLXML.4.0" 합니다.  
  
  
