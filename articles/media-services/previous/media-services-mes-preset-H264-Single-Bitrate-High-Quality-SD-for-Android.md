---
title: H264 Single Bitrate hoge kwaliteit SD voor Android | Microsoft Docs
description: Het onderwerp een overzicht van de **H264 één bitsnelheid van hoge kwaliteit SD voor Android** taak vooraf ingesteld.
author: Juliako
manager: femila
editor: ''
services: media-services
documentationcenter: ''
ms.assetid: 4a190f24-ec6a-47e7-8bca-6294e064b15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/30/2018
ms.author: juliako
ms.openlocfilehash: 098bf237953530a09bc454a921ae5d5a399f3315
ms.sourcegitcommit: 1d3353b95e0de04d4aec2d0d6f84ec45deaaf6ae
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/30/2018
ms.locfileid: "50250781"
---
# <a name="h264-single-bitrate-high-quality-sd-for-android"></a>H264 Één bitsnelheid van hoge kwaliteit SD voor Android
`Media Encoder Standard` definieert een reeks voorinstellingen die kunt u bij het maken van coderingstaken coderen. Kunt u ofwel een `preset name` om op te geven in welke indeling u wilt coderen van uw media-bestand. Of, kunt u uw eigen JSON of XML-indeling voorinstellingen (met behulp van UTF-8- of UTF-16-codering. Vervolgens geeft u door de aangepaste voorinstelling voor het coderingsprogramma. Voor een lijst van de vooraf gedefinieerde namen ondersteund door dit `Media Encoder Standard` encoder, Zie [taak voorinstellingen voor Media Encoder Standard](media-services-mes-presets-overview.md).  
  
 In dit onderwerp leest de `H264 Single Bitrate High Quality SD for Android` vooraf in XML en JSON-indeling.  
  
 Deze vooraf ingestelde produceert een enkel MP4-bestand met een bitrate van 500 kbps en stereo AAC-audio. Voor gedetailleerde informatie over het profiel bitrate, steekproeven snelheid, enz. van deze vooraf ingesteld, controleert u de XML of JSON hieronder gedefinieerd. Voor een uitleg van wat elk element in deze middelen voorinstellingen, en de geldige waarden voor elk element, Zie de [Media Encoder Standard schema](media-services-mes-schema.md) onderwerp.  
  
 XML  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:05</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>500</Bitrate>  
          <Width>480</Width>  
          <Height>360</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Baseline</Profile>  
          <Level>3</Level>  
          <BFrames>0</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>false</AdaptiveBFrame>  
          <EntropyMode>Cavlc</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>500</MaxBitrate>  
        </H264Layer>  
      </H264Layers>  
      <Chapters />  
    </H264Video>  
    <AACAudio>  
      <Profile>AACLC</Profile>  
      <Channels>2</Channels>  
      <SamplingRate>48000</SamplingRate>  
      <Bitrate>128</Bitrate>  
    </AACAudio>  
  </Encoding>  
  <Outputs>  
    <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">  
      <MP4Format />  
    </Output>  
  </Outputs>  
</Preset>  
```  
  
 JSON  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:05",  
      "SceneChangeDetection": true,  
      "H264Layers": [  
        {  
          "Profile": "Baseline",  
          "Level": "3",  
          "Bitrate": 500,  
          "MaxBitrate": 500,  
          "BufferWindow": "00:00:05",  
          "Width": 480,  
          "Height": 360,  
          "ReferenceFrames": 3,  
          "EntropyMode": "Cavlc",  
          "Type": "H264Layer",  
          "FrameRate": "0/1"  
        }  
      ],  
      "Type": "H264Video"  
    },  
    {  
      "Profile": "AACLC",  
      "Channels": 2,  
      "SamplingRate": 48000,  
      "Bitrate": 128,  
      "Type": "AACAudio"  
    }  
  ],  
  "Outputs": [  
    {  
      "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",  
      "Format": {  
        "Type": "MP4Format"  
      }  
    }  
  ]  
}  
```
