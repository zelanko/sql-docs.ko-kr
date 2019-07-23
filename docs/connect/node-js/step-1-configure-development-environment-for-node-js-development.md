---
title: '1단계: Node.js 개발을 위한 개발 환경 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2dad01f1-fadf-4ac9-9b4d-26be3d301886
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bce89cc12c7493522de55adffb69fcbe3307cbdf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003763"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>1단계: Node.js 개발을 위한 개발 환경 구성
SQL Server에 대 한 node.js 드라이버를 사용 하 여 응용 프로그램을 개발 하려면 필수 구성 요소를 사용 하 여 개발 환경을 구성 해야 합니다.  가장 일반적인 방법은 npm (node package manager)를 사용 하 여 지루한 모듈을 설치 하는 것 이지만 원하는 경우 [Github](https://github.com/pekim/tedious) 에서 직접 지루한 모듈을 다운로드할 수 있습니다.  
  
Node.js 드라이버는 SQL Server 및 Azure SQL Database에서 기본적으로 사용 되는 TDS 프로토콜을 사용 합니다.  추가적인 서버 구성은 필요하지 않습니다.  
  
## <a name="windows"></a>Windows  
  
1. **Node.js 런타임 및 npm 패키지 관리자를 설치 합니다.**  
1\. [Node.js](https://nodejs.org/en/download/) 로 이동  
2\. 적절 한 Windows installer msi 링크를 클릭 합니다.   
c. 다운로드가 완료 되 면 msi를 실행 하 여 node.js를 설치 합니다.  
  
2. **Cmd.exe를 엽니다.**  
  
3. **프로젝트 디렉터리를 만들고** 이동 합니다.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **노드 프로젝트를 만듭니다.**  프로젝트를 만드는 동안 기본값을 유지 하려면 프로젝트를 만들 때까지 enter 키를 누릅니다. 이 단계가 끝나면 프로젝트 디렉터리에 package. json 파일이 표시 됩니다.  
```  
> npm init  
```  
  
5. **프로젝트에 지루한 모듈을 설치 합니다.**  드라이버가 SQL Server와 통신 하는 데 사용 하는 TDS 프로토콜의 구현입니다.  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **터미널 열기**  
  
2. **Node.js 런타임 설치**  
```  
>sudo apt-get install node  
```  
3. **Npm 설치 (노드 패키지 관리자)**  
```  
> sudo apt-get install npm  
```  
4. **프로젝트 디렉터리를 만들고** 이동 합니다.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **노드 프로젝트를 만듭니다.**  프로젝트를 만드는 동안 기본값을 유지 하려면 프로젝트를 만들 때까지 enter 키를 누릅니다. 이 단계가 끝나면 프로젝트 디렉터리에 package. json 파일이 표시 됩니다.  
```  
> sudo npm init  
```  
  
6. **프로젝트에 지루한 모듈을 설치 합니다.**  드라이버가 SQL Server와 통신 하는 데 사용 하는 TDS 프로토콜의 구현입니다.  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **Node.js 런타임 및 npm 패키지 관리자를 설치 합니다.**  
1\. [Node.js](https://nodejs.org/en/download/) 로 이동  
2\. 적절 한 Mac OS 설치 관리자 링크를 클릭 합니다.  
c. 다운로드 한 후 dmg를 실행 하 여 node.js를 설치 합니다.  
  
2. **터미널 열기**  
  
3. **프로젝트 디렉터리를 만들고** 이동 합니다.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **노드 프로젝트를 만듭니다.**  프로젝트를 만드는 동안 기본값을 유지 하려면 프로젝트를 만들 때까지 enter 키를 누릅니다. 이 단계가 끝나면 프로젝트 디렉터리에 package. json 파일이 표시 됩니다.  
```  
> npm init  
```  
  
5. **프로젝트에 지루한 모듈을 설치 합니다.**  드라이버가 SQL Server와 통신 하는 데 사용 하는 TDS 프로토콜의 구현입니다.  
```  
> npm install tedious  
```  
  
