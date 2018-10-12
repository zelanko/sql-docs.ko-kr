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
manager: craigg
ms.openlocfilehash: 823177f8fef91dda8cf879f6be84ef6706224fad
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600241"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>1단계: Node.js 개발을 위한 개발 환경 구성
SQL Server 용 Node.js 드라이버를 사용 하 여 응용 프로그램을 개발 하기 위해 개발 환경 필수 구성 요소를 사용 하 여 구성 해야 합니다.  가장 일반적인 방법은 지루한 모듈을 설치 하 고 노드 패키지 관리자 (npm)를 사용 하는 것 이지만 지루한 모듈에서 직접 다운로드할 수 있습니다 [Github](https://github.com/pekim/tedious) 하려는 경우.  
  
Node.js 드라이버를 SQL Server 및 Azure SQL Database에 기본적으로 사용 되는 TDS 프로토콜을 사용 하는 참고 합니다.  추가적인 서버 구성은 필요하지 않습니다.  
  
## <a name="windows"></a>Windows  
  
1. **Node.js 런타임 및 npm 패키지 관리자 설치**  
1. 로 [Node.js](https://nodejs.org/en/download/)  
2. 적절 한 Windows installer msi 링크를 클릭 합니다.   
c. 다운로드 한 후 Node.js를 설치 하는 msi를 실행  
  
2. **Cmd.exe를 열으십시오**  
  
3. **프로젝트 디렉터리를 만듭니다** 폴더로 이동 합니다.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **노드 프로젝트를 만듭니다.**  프로젝트를 만드는 동안 기본값을 유지 하기 위해 프로젝트를 만들 때까지 enter 키를 누릅니다. 이 단계의 끝 package.json 파일을 프로젝트 디렉터리에 표시 됩니다.  
```  
> npm init  
```  
  
5. **프로젝트의 지루한 작업 모듈을 설치 합니다.**  SQL Server와 통신 하는 드라이버를 사용 하는 TDS 프로토콜의 구현입니다.  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **터미널 열기**  
  
2. **Node.js 런타임을 설치합니다**  
```  
>sudo apt-get install node  
```  
3. **Npm (노드 패키지 관리자)를 설치 합니다.**  
```  
> sudo apt-get install npm  
```  
4. **프로젝트 디렉터리를 만듭니다** 폴더로 이동 합니다.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **노드 프로젝트를 만듭니다.**  프로젝트를 만드는 동안 기본값을 유지 하기 위해 프로젝트를 만들 때까지 enter 키를 누릅니다. 이 단계의 끝 package.json 파일을 프로젝트 디렉터리에 표시 됩니다.  
```  
> sudo npm init  
```  
  
6. **프로젝트의 지루한 작업 모듈을 설치 합니다.**  SQL Server와 통신 하는 드라이버를 사용 하는 TDS 프로토콜의 구현입니다.  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **Node.js 런타임 및 npm 패키지 관리자 설치**  
1. 로 [Node.js](https://nodejs.org/en/download/)  
2. 적절 한 Mac 운영 체제 설치 관리자 링크를 클릭 합니다.  
c. 다운로드 한 후 실행 dmg Node.js를 설치 하려면  
  
2. **터미널 열기**  
  
3. **프로젝트 디렉터리를 만듭니다** 폴더로 이동 합니다.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **노드 프로젝트를 만듭니다.**  프로젝트를 만드는 동안 기본값을 유지 하기 위해 프로젝트를 만들 때까지 enter 키를 누릅니다. 이 단계의 끝 package.json 파일을 프로젝트 디렉터리에 표시 됩니다.  
```  
> npm init  
```  
  
5. **프로젝트의 지루한 작업 모듈을 설치 합니다.**  SQL Server와 통신 하는 드라이버를 사용 하는 TDS 프로토콜의 구현입니다.  
```  
> npm install tedious  
```  
  
