---
title: Haplotype, LD, and Association Tests
author: Sichong Peng
date: '2019-03-21'
slug: haplotype-ld-and-association-tests
categories:
  - Genetics
tags:
  - Population Genetics
  - QE
  - Statistics
image:
  caption: ''
  focal_point: ''
math: true
toc: true
---


_This is the first post of my QE prep series. I'll be taking notes on my study for general knowledge section of my QE. I'm gonna start this off with my favorite topic in our GGG series classes: population genetics_

## Haplotype and Linkage Disequilibrium (LD)
To properly understand linkage disequilibrium, I want to go back to the "Dark Age" of genetics, when Gregor Mendel brilliantly discovered (Mendelian) laws of inheritance without any knowledge of the molecular basis.

- The First Mendelian Law (Law of Segregation) states that each organism has two alleles for each trait and one of the two alleles is randomly passed on to an offspring during sexual reproduction.

    - For example, an individual with an AB genotype is eqaully likely to pass an `A` allele or a `B` allele to its offspring (there are many assumption being made in this statement but I'll roll with it for now).

- The Second Mendelian Law (Law of Independent Assortment) states that alleles for different traits are passed on independantly from each other during sexual reproduction.

    - For example, if allelea `A/a` controls for trait 1 and alleles `B/b` controls for trait 2 (assuming they are not at the same locus), then whether an individual passes on allele `A` or `a` is independent of wheter it passes on `B` or `b`. The Independent Assortment implicts the product rule:

        >Suppose an individual with `AaBb` genotype (`Aa` at locus 1 and `Bb` at locus 2) mates with another individual with same `AaBb` genotype, the probability of their offspring being `aabb` is `1/16`

    - In case you're wondering how to get this number, here is my favorite way to calculate:


<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI0NDJweCIgaGVpZ2h0PSIzOTJweCIgdmlld0JveD0iLTAuNSAtMC41IDQ0MiAzOTIiPjxkZWZzLz48Zz48cmVjdCB4PSIxMzAiIHk9IjAiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNzQuNSwyMy41KSI+PHN3aXRjaD48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6dmlzaWJsZTsiIHBvaW50ZXItZXZlbnRzPSJhbGwiIHdpZHRoPSIzMCIgaGVpZ2h0PSIxMiIgcmVxdWlyZWRGZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiByZ2IoMCwgMCwgMCk7IGxpbmUtaGVpZ2h0OiAxLjI7IHZlcnRpY2FsLWFsaWduOiB0b3A7IHdpZHRoOiAzMHB4OyB3aGl0ZS1zcGFjZTogbm93cmFwOyBvdmVyZmxvdy13cmFwOiBub3JtYWw7IHRleHQtYWxpZ246IGNlbnRlcjsiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OmlubGluZS1ibG9jazt0ZXh0LWFsaWduOmluaGVyaXQ7dGV4dC1kZWNvcmF0aW9uOmluaGVyaXQ7Ij5BYUJiPC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0Pjx0ZXh0IHg9IjE1IiB5PSIxMiIgZmlsbD0iIzAwMDAwMCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMnB4IiBmb250LWZhbWlseT0iSGVsdmV0aWNhIj5BYUJiPC90ZXh0Pjwvc3dpdGNoPjwvZz48cmVjdCB4PSIzMjAiIHk9IjAiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgzNjQuNSwyMy41KSI+PHN3aXRjaD48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6dmlzaWJsZTsiIHBvaW50ZXItZXZlbnRzPSJhbGwiIHdpZHRoPSIzMCIgaGVpZ2h0PSIxMiIgcmVxdWlyZWRGZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiByZ2IoMCwgMCwgMCk7IGxpbmUtaGVpZ2h0OiAxLjI7IHZlcnRpY2FsLWFsaWduOiB0b3A7IHdpZHRoOiAzMHB4OyB3aGl0ZS1zcGFjZTogbm93cmFwOyBvdmVyZmxvdy13cmFwOiBub3JtYWw7IHRleHQtYWxpZ246IGNlbnRlcjsiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OmlubGluZS1ibG9jazt0ZXh0LWFsaWduOmluaGVyaXQ7dGV4dC1kZWNvcmF0aW9uOmluaGVyaXQ7Ij5BYUJiPC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0Pjx0ZXh0IHg9IjE1IiB5PSIxMiIgZmlsbD0iIzAwMDAwMCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMnB4IiBmb250LWZhbWlseT0iSGVsdmV0aWNhIj5BYUJiPC90ZXh0Pjwvc3dpdGNoPjwvZz48cGF0aCBkPSJNIDE5MC4xNCA2MC4yOSBMIDE5MC4wMiAxMDMuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMTkwIDEwOC44OCBMIDE4Ni41MiAxMDEuODcgTCAxOTAuMDIgMTAzLjYzIEwgMTkzLjUyIDEwMS44OSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxMzMuNSwxMTMuNSkiPjxzd2l0Y2g+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OnZpc2libGU7IiBwb2ludGVyLWV2ZW50cz0iYWxsIiB3aWR0aD0iMzIiIGhlaWdodD0iMTIiIHJlcXVpcmVkRmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogcmdiKDAsIDAsIDApOyBsaW5lLWhlaWdodDogMS4yOyB2ZXJ0aWNhbC1hbGlnbjogdG9wOyB3aWR0aDogMzJweDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgb3ZlcmZsb3ctd3JhcDogbm9ybWFsOyB0ZXh0LWFsaWduOiBjZW50ZXI7Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTppbmxpbmUtYmxvY2s7dGV4dC1hbGlnbjppbmhlcml0O3RleHQtZGVjb3JhdGlvbjppbmhlcml0OyI+QTogMS8yPC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0Pjx0ZXh0IHg9IjE2IiB5PSIxMiIgZmlsbD0iIzAwMDAwMCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMnB4IiBmb250LWZhbWlseT0iSGVsdmV0aWNhIj5BOiAxLzI8L3RleHQ+PC9zd2l0Y2g+PC9nPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEzNC41LDE1My41KSI+PHN3aXRjaD48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6dmlzaWJsZTsiIHBvaW50ZXItZXZlbnRzPSJhbGwiIHdpZHRoPSIzMCIgaGVpZ2h0PSIxMiIgcmVxdWlyZWRGZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiByZ2IoMCwgMCwgMCk7IGxpbmUtaGVpZ2h0OiAxLjI7IHZlcnRpY2FsLWFsaWduOiB0b3A7IHdpZHRoOiAzMXB4OyB3aGl0ZS1zcGFjZTogbm93cmFwOyBvdmVyZmxvdy13cmFwOiBub3JtYWw7IHRleHQtYWxpZ246IGNlbnRlcjsiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OmlubGluZS1ibG9jazt0ZXh0LWFsaWduOmluaGVyaXQ7dGV4dC1kZWNvcmF0aW9uOmluaGVyaXQ7Ij5hOiAxLzI8L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PHRleHQgeD0iMTUiIHk9IjEyIiBmaWxsPSIjMDAwMDAwIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjEycHgiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiPmE6IDEvMjwvdGV4dD48L3N3aXRjaD48L2c+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMjA5LjUsMTUzLjUpIj48c3dpdGNoPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzp2aXNpYmxlOyIgcG9pbnRlci1ldmVudHM9ImFsbCIgd2lkdGg9IjMwIiBoZWlnaHQ9IjEyIiByZXF1aXJlZEZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6IHJnYigwLCAwLCAwKTsgbGluZS1oZWlnaHQ6IDEuMjsgdmVydGljYWwtYWxpZ246IHRvcDsgd2lkdGg6IDMxcHg7IHdoaXRlLXNwYWNlOiBub3dyYXA7IG92ZXJmbG93LXdyYXA6IG5vcm1hbDsgdGV4dC1hbGlnbjogY2VudGVyOyI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6aW5saW5lLWJsb2NrO3RleHQtYWxpZ246aW5oZXJpdDt0ZXh0LWRlY29yYXRpb246aW5oZXJpdDsiPmI6IDEvMjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48dGV4dCB4PSIxNSIgeT0iMTIiIGZpbGw9IiMwMDAwMDAiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTJweCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSI+YjogMS8yPC90ZXh0Pjwvc3dpdGNoPjwvZz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgyMDguNSwxMTMuNSkiPjxzd2l0Y2g+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OnZpc2libGU7IiBwb2ludGVyLWV2ZW50cz0iYWxsIiB3aWR0aD0iMzIiIGhlaWdodD0iMTIiIHJlcXVpcmVkRmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogcmdiKDAsIDAsIDApOyBsaW5lLWhlaWdodDogMS4yOyB2ZXJ0aWNhbC1hbGlnbjogdG9wOyB3aWR0aDogMzJweDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgb3ZlcmZsb3ctd3JhcDogbm9ybWFsOyB0ZXh0LWFsaWduOiBjZW50ZXI7Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTppbmxpbmUtYmxvY2s7dGV4dC1hbGlnbjppbmhlcml0O3RleHQtZGVjb3JhdGlvbjppbmhlcml0OyI+QjogMS8yPC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0Pjx0ZXh0IHg9IjE2IiB5PSIxMiIgZmlsbD0iIzAwMDAwMCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMnB4IiBmb250LWZhbWlseT0iSGVsdmV0aWNhIj5COiAxLzI8L3RleHQ+PC9zd2l0Y2g+PC9nPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDMyNi41LDExMy41KSI+PHN3aXRjaD48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6dmlzaWJsZTsiIHBvaW50ZXItZXZlbnRzPSJhbGwiIHdpZHRoPSIzMiIgaGVpZ2h0PSIxMiIgcmVxdWlyZWRGZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiByZ2IoMCwgMCwgMCk7IGxpbmUtaGVpZ2h0OiAxLjI7IHZlcnRpY2FsLWFsaWduOiB0b3A7IHdpZHRoOiAzMnB4OyB3aGl0ZS1zcGFjZTogbm93cmFwOyBvdmVyZmxvdy13cmFwOiBub3JtYWw7IHRleHQtYWxpZ246IGNlbnRlcjsiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OmlubGluZS1ibG9jazt0ZXh0LWFsaWduOmluaGVyaXQ7dGV4dC1kZWNvcmF0aW9uOmluaGVyaXQ7Ij5BOiAxLzI8L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PHRleHQgeD0iMTYiIHk9IjEyIiBmaWxsPSIjMDAwMDAwIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjEycHgiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiPkE6IDEvMjwvdGV4dD48L3N3aXRjaD48L2c+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMzI3LjUsMTUzLjUpIj48c3dpdGNoPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzp2aXNpYmxlOyIgcG9pbnRlci1ldmVudHM9ImFsbCIgd2lkdGg9IjMwIiBoZWlnaHQ9IjEyIiByZXF1aXJlZEZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6IHJnYigwLCAwLCAwKTsgbGluZS1oZWlnaHQ6IDEuMjsgdmVydGljYWwtYWxpZ246IHRvcDsgd2lkdGg6IDMxcHg7IHdoaXRlLXNwYWNlOiBub3dyYXA7IG92ZXJmbG93LXdyYXA6IG5vcm1hbDsgdGV4dC1hbGlnbjogY2VudGVyOyI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6aW5saW5lLWJsb2NrO3RleHQtYWxpZ246aW5oZXJpdDt0ZXh0LWRlY29yYXRpb246aW5oZXJpdDsiPmE6IDEvMjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48dGV4dCB4PSIxNSIgeT0iMTIiIGZpbGw9IiMwMDAwMDAiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTJweCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSI+YTogMS8yPC90ZXh0Pjwvc3dpdGNoPjwvZz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSg0MDIuNSwxNTMuNSkiPjxzd2l0Y2g+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OnZpc2libGU7IiBwb2ludGVyLWV2ZW50cz0iYWxsIiB3aWR0aD0iMzAiIGhlaWdodD0iMTIiIHJlcXVpcmVkRmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogcmdiKDAsIDAsIDApOyBsaW5lLWhlaWdodDogMS4yOyB2ZXJ0aWNhbC1hbGlnbjogdG9wOyB3aWR0aDogMzFweDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgb3ZlcmZsb3ctd3JhcDogbm9ybWFsOyB0ZXh0LWFsaWduOiBjZW50ZXI7Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTppbmxpbmUtYmxvY2s7dGV4dC1hbGlnbjppbmhlcml0O3RleHQtZGVjb3JhdGlvbjppbmhlcml0OyI+YjogMS8yPC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0Pjx0ZXh0IHg9IjE1IiB5PSIxMiIgZmlsbD0iIzAwMDAwMCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMnB4IiBmb250LWZhbWlseT0iSGVsdmV0aWNhIj5iOiAxLzI8L3RleHQ+PC9zd2l0Y2g+PC9nPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDQwMS41LDExMy41KSI+PHN3aXRjaD48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6dmlzaWJsZTsiIHBvaW50ZXItZXZlbnRzPSJhbGwiIHdpZHRoPSIzMiIgaGVpZ2h0PSIxMiIgcmVxdWlyZWRGZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiByZ2IoMCwgMCwgMCk7IGxpbmUtaGVpZ2h0OiAxLjI7IHZlcnRpY2FsLWFsaWduOiB0b3A7IHdpZHRoOiAzMnB4OyB3aGl0ZS1zcGFjZTogbm93cmFwOyBvdmVyZmxvdy13cmFwOiBub3JtYWw7IHRleHQtYWxpZ246IGNlbnRlcjsiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OmlubGluZS1ibG9jazt0ZXh0LWFsaWduOmluaGVyaXQ7dGV4dC1kZWNvcmF0aW9uOmluaGVyaXQ7Ij5COiAxLzI8L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PHRleHQgeD0iMTYiIHk9IjEyIiBmaWxsPSIjMDAwMDAwIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjEycHgiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiPkI6IDEvMjwvdGV4dD48L3N3aXRjaD48L2c+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC41LDEyMC41KSI+PHN3aXRjaD48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6dmlzaWJsZTsiIHBvaW50ZXItZXZlbnRzPSJhbGwiIHdpZHRoPSIxMTgiIGhlaWdodD0iMzgiIHJlcXVpcmVkRmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxN3B4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogcmdiKDAsIDAsIDApOyBsaW5lLWhlaWdodDogMS4yOyB2ZXJ0aWNhbC1hbGlnbjogdG9wOyB3aWR0aDogMTE4cHg7IHdoaXRlLXNwYWNlOiBub3JtYWw7IG92ZXJmbG93LXdyYXA6IG5vcm1hbDsgZm9udC13ZWlnaHQ6IGJvbGQ7IHRleHQtYWxpZ246IGNlbnRlcjsiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OmlubGluZS1ibG9jazt0ZXh0LWFsaWduOmluaGVyaXQ7dGV4dC1kZWNvcmF0aW9uOmluaGVyaXQ7Ij5MYXcgb2YgU2VncmVnYXRpb248L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PHRleHQgeD0iNTkiIHk9IjI4IiBmaWxsPSIjMDAwMDAwIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjE3cHgiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIj5MYXcgb2YgU2VncmVnYXRpb248L3RleHQ+PC9zd2l0Y2g+PC9nPjxwYXRoIGQ9Ik0gMzgwIDYwIEwgMzgwIDEwMy42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAzODAgMTA4Ljg4IEwgMzc2LjUgMTAxLjg4IEwgMzgwIDEwMy42MyBMIDM4My41IDEwMS44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZWxsaXBzZSBjeD0iMTUwIiBjeT0iMTYwIiByeD0iMjIuNSIgcnk9IjE1LjAwMDAwMDAwMDAwMDAwMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjZmYwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxlbGxpcHNlIGN4PSIyMjUiIGN5PSIxNjAiIHJ4PSIyMi41IiByeT0iMTUuMDAwMDAwMDAwMDAwMDAyIiBmaWxsPSJub25lIiBzdHJva2U9IiNmZjAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGVsbGlwc2UgY3g9IjM0NSIgY3k9IjE2MCIgcng9IjIyLjUiIHJ5PSIxNS4wMDAwMDAwMDAwMDAwMDIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iI2ZmMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZWxsaXBzZSBjeD0iNDE1IiBjeT0iMTYwIiByeD0iMjIuNSIgcnk9IjE1LjAwMDAwMDAwMDAwMDAwMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjZmYwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMTUwIDE3NSBMIDE4NS43NyAyMTUuMjQiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMTg5LjI2IDIxOS4xNiBMIDE4MS45OSAyMTYuMjYgTCAxODUuNzcgMjE1LjI0IEwgMTg3LjIyIDIxMS42MSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDIyNC40MyAxNzQuNTcgTCAxOTMuODUgMjE0LjkyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDE5MC42OCAyMTkuMTEgTCAxOTIuMTEgMjExLjQyIEwgMTkzLjg1IDIxNC45MiBMIDE5Ny42OSAyMTUuNjQgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGVsbGlwc2UgY3g9IjE5MCIgY3k9IjI0MCIgcng9IjMxLjQ5OTk5OTk5OTk5OTk5NiIgcnk9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMTY1LjUsMjMwLjUpIj48c3dpdGNoPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzp2aXNpYmxlOyIgcG9pbnRlci1ldmVudHM9ImFsbCIgd2lkdGg9IjUyIiBoZWlnaHQ9IjE4IiByZXF1aXJlZEZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTdweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6IHJnYigwLCAwLCAwKTsgbGluZS1oZWlnaHQ6IDEuMjsgdmVydGljYWwtYWxpZ246IHRvcDsgd2lkdGg6IDUzcHg7IHdoaXRlLXNwYWNlOiBub3dyYXA7IG92ZXJmbG93LXdyYXA6IG5vcm1hbDsgdGV4dC1hbGlnbjogY2VudGVyOyI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6aW5saW5lLWJsb2NrO3RleHQtYWxpZ246aW5oZXJpdDt0ZXh0LWRlY29yYXRpb246aW5oZXJpdDsiPmFiOiAxLzQ8L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PHRleHQgeD0iMjYiIHk9IjE4IiBmaWxsPSIjMDAwMDAwIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjE3cHgiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiPmFiOiAxLzQ8L3RleHQ+PC9zd2l0Y2g+PC9nPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDguNSwxOTAuNSkiPjxzd2l0Y2g+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OnZpc2libGU7IiBwb2ludGVyLWV2ZW50cz0iYWxsIiB3aWR0aD0iMTE4IiBoZWlnaHQ9IjU4IiByZXF1aXJlZEZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTdweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6IHJnYigwLCAwLCAwKTsgbGluZS1oZWlnaHQ6IDEuMjsgdmVydGljYWwtYWxpZ246IHRvcDsgd2lkdGg6IDExOHB4OyB3aGl0ZS1zcGFjZTogbm9ybWFsOyBvdmVyZmxvdy13cmFwOiBub3JtYWw7IGZvbnQtd2VpZ2h0OiBib2xkOyB0ZXh0LWFsaWduOiBjZW50ZXI7Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTppbmxpbmUtYmxvY2s7dGV4dC1hbGlnbjppbmhlcml0O3RleHQtZGVjb3JhdGlvbjppbmhlcml0OyI+TGF3IG9mIEluZGVwZW5kZW50IEFzc29ydG1lbnTCoDwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48dGV4dCB4PSI1OSIgeT0iMzgiIGZpbGw9IiMwMDAwMDAiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTdweCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC13ZWlnaHQ9ImJvbGQiPltOb3Qgc3VwcG9ydGVkIGJ5IHZpZXdlcl08L3RleHQ+PC9zd2l0Y2g+PC9nPjxwYXRoIGQ9Ik0gMzQ1IDE3NSBMIDM4MC43NyAyMTUuMjQiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMzg0LjI2IDIxOS4xNiBMIDM3Ni45OSAyMTYuMjYgTCAzODAuNzcgMjE1LjI0IEwgMzgyLjIyIDIxMS42MSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDQxOS43NiAxNzQuNDcgTCAzODguODYgMjE0Ljk0IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDM4NS42OCAyMTkuMTEgTCAzODcuMTQgMjExLjQyIEwgMzg4Ljg2IDIxNC45NCBMIDM5Mi43MSAyMTUuNjcgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGVsbGlwc2UgY3g9IjM4NSIgY3k9IjI0MCIgcng9IjMxLjQ5OTk5OTk5OTk5OTk5NiIgcnk9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMzU5LjUsMjMwLjUpIj48c3dpdGNoPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzp2aXNpYmxlOyIgcG9pbnRlci1ldmVudHM9ImFsbCIgd2lkdGg9IjUyIiBoZWlnaHQ9IjE4IiByZXF1aXJlZEZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTdweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6IHJnYigwLCAwLCAwKTsgbGluZS1oZWlnaHQ6IDEuMjsgdmVydGljYWwtYWxpZ246IHRvcDsgd2lkdGg6IDUzcHg7IHdoaXRlLXNwYWNlOiBub3dyYXA7IG92ZXJmbG93LXdyYXA6IG5vcm1hbDsgdGV4dC1hbGlnbjogY2VudGVyOyI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6aW5saW5lLWJsb2NrO3RleHQtYWxpZ246aW5oZXJpdDt0ZXh0LWRlY29yYXRpb246aW5oZXJpdDsiPmFiOiAxLzQ8L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PHRleHQgeD0iMjYiIHk9IjE4IiBmaWxsPSIjMDAwMDAwIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjE3cHgiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiPmFiOiAxLzQ8L3RleHQ+PC9zd2l0Y2g+PC9nPjxwYXRoIGQ9Ik0gMTkxLjUgMjYwIEwgMjc1LjI4IDMzNS43MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyNzkuMTcgMzM5LjI1IEwgMjcxLjYzIDMzNy4xNSBMIDI3NS4yOCAzMzUuNzMgTCAyNzYuMzIgMzMxLjk2IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMzg1IDI2MCBMIDI4NS4wNyAzMzYuMTQiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMjgwLjg5IDMzOS4zMiBMIDI4NC4zNCAzMzIuMyBMIDI4NS4wNyAzMzYuMTQgTCAyODguNTggMzM3Ljg2IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxlbGxpcHNlIGN4PSIyODAiIGN5PSIzNjUiIHJ4PSI2MC4wMDAwMDAwMDAwMDAwMSIgcnk9IjI1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMjM5LjUsMzU1LjUpIj48c3dpdGNoPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzp2aXNpYmxlOyIgcG9pbnRlci1ldmVudHM9ImFsbCIgd2lkdGg9IjgxIiBoZWlnaHQ9IjE4IiByZXF1aXJlZEZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTdweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6IHJnYigwLCAwLCAwKTsgbGluZS1oZWlnaHQ6IDEuMjsgdmVydGljYWwtYWxpZ246IHRvcDsgd2lkdGg6IDgycHg7IHdoaXRlLXNwYWNlOiBub3dyYXA7IG92ZXJmbG93LXdyYXA6IG5vcm1hbDsgdGV4dC1hbGlnbjogY2VudGVyOyI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6aW5saW5lLWJsb2NrO3RleHQtYWxpZ246aW5oZXJpdDt0ZXh0LWRlY29yYXRpb246aW5oZXJpdDsiPmFhYmI6IDEvMTY8L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PHRleHQgeD0iNDEiIHk9IjE4IiBmaWxsPSIjMDAwMDAwIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjE3cHgiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiPmFhYmI6IDEvMTY8L3RleHQ+PC9zd2l0Y2g+PC9nPjwvZz48L3N2Zz4=" />

  _In the above diagram, first step involves the Law of Segregation, by which I calculated the probability of each gamete containing each allele separately. The second step is where the Law of Independent Assortment comes into play: The probability of each combination of two alleles is the product of the probabilities of each allele (in one gamete). And the last step is just random combination of two gametes (for a diploid organism)._


However, just as every law has an exception, it was discovered that many of traits in various species didn't really follow the Law of Independent Assortment. The following example shows a case of "dependent assortment":

  > Sweet peas have purple (`P`) or red (`p`) flowers and long (`L`) or short (`l`) pollen grains. Peas from two pure lines (`PPLL` and `ppll`) were crossed. The offspring (F1) are all purple flower and long grain (PpLl). They are then self crossed (`PpLl` X `PpLl`).

  > Assuming indenpendent assortment, we expect to observe all 4 phenotypes in F2 with the following frequencies:

|Phenotype|Frequency|
|---|---|
|Purple (P_), Long (L_)|9/16|
|Purple (P_), Short (ll)|3/16|
|Red (pp), Long (L_)|3/16|
|Red (pp), Short (ll)|1/16|

>However, large deviations from expected phenotype frequency were observed:

|Phenotype|Exp. Count|Obs. Count|
|---|---|---|
|Purple, Long (P\_L_)|216|284|
|Purple, Short (P_ll)|72|21|
|Red, Long (ppL_)|72|21|
|Red, Short (ppll)|24|55|
_Data from Bateson et al._

We know that in the parent line (`PPLL x ppll`) `P` and `L` as well as `p` and `l` are always together because they are both homozygotes. But as the Mendel's second law predicts, they should've independently assorted from F1 to F2. We, however, see that instead of random combination, `P` still appear more often together with `L` and so does `p` and `l`. It's as if `P` and `L` were somehow linked. This phenomenon is termed [`Linkage`](https://en.wikipedia.org/wiki/Genetic_linkage). We now know that this is because the two loci are closeby on the same chromsome and that during [meiosis](https://en.wikipedia.org/wiki/Meiosis), DNA on one chromsome are largely segregated together (except some [recombination](https://en.wikipedia.org/wiki/Genetic_recombination)).

When two loci are linked, product rule no longer applies. This causes a non-random association of alleles at different loci in a **given population**. This is termed `Linkage Disequilibrium` or `LD`.

When we talk about linkage, knowing genotype of an individual alone is no longer enough: we wish to know which alleles are "linked" or belong to the same chromsome. In genetics, we call alleles that are on the same chromsome and likely to be inherited together a haplotype. For example, an individual with a `PpLl` genotype may have these different haplotypes:

  - `PL` and `pl`
  - `Pl` and `pL`

There are several different ways to quntify the extent of linkage between any **two** loci:

- Coefficient of Linkage Disequilibrium (D)
- Normalized coefficient of Linkage Disequilibrium (D')
- Correlation coefficient ($r^2$) and $\chi^2$ test

I'll briefly go over them below.

### Linkage Disequilibrium Coefficient (D):
As mentioned before, if two loci are independent, their frequencies follow product rule:

   For two independent loci A and B, each with two alleles ($A_1$, $A_2$ and $B_1$, $B_2$, respectively), we have:
    $$f\_{A\_1B\_1} = f\_{A\_1}f\_{B\_1}$$
   Now if A and B are not independent, this equation no longer stands true. In that case we have:
    $$f\_{A\_1B\_1} = f\_{A\_1}f\_{B\_1} + D$$
  Here we have D as a _measurement_ of the extent of linkage disequilibrium between $A\_1$ and $B\_1$. We can calculate the same for all 4 haplotypes:

|   |A|$A\_1$|$A\_2$|
|---|---|---|---|
|B|frequency|$f\_{A\_1}$|$f\_{A\_2}$|
|$B\_1$|$f\_{B\_1}$|$f\_{A\_1}f\_{B\_1} + D\_{A\_1B\_1}$|$f\_{A\_2}f\_{B\_1} + D\_{A\_2B\_1}$|
|$B\_2$|$f\_{B\_2}$|$f\_{A\_1}f\_{B\_2} + D\_{A\_1B\_2}$|$f\_{A\_2}f\_{B\_2} + D\_{A\_2B\_2}$|
Solve above equations and we get:

> $D\_{A\_1B\_1} = f\_{A\_1B\_1} - f\_{A\_1}f\_{B\_1}$

> $D\_{A\_1B\_2} = f\_{A\_1B\_2} - f\_{A\_1}f\_{B\_2}$

> $D\_{A\_2B\_1} = f\_{A\_2B\_1} - f\_{A\_2}f\_{B\_1}$

> $D\_{A\_2B\_2} = f\_{A\_2B\_2} - f\_{A\_2}f\_{B\_2}$

For a given population, we have

> $f\_{A\_1} + f\_{A\_2} = 1$

> $f\_{B\_1} + f\_{B\_2} = 1$

> $f\_{A\_1B\_1} + f\_{A\_1B\_2} = f\_{A\_1}$

> $f\_{A\_1B\_1} + f\_{A\_2B\_1} = f\_{B\_1}$

> $f\_{A\_2B\_1} + f\_{A\_2B\_2} = f\_{A\_2} = 1 - f\_{A\_1}$

> $f\_{A\_1B\_2} + f\_{A\_2B\_2} = f\_{B\_2} = 1 - f\_{B\_1}$

We can then further derive above equations:

> $D\_{A\_2B\_2} \\\\\\ = f\_{A\_2B\_2} - (1 - f\_{A\_1})(1 - f\_{B\_1})
 \\\\\\\ = 1 - f\_{B\_1} - f\_{A\_1B\_2} - (1 - f\_{A\_1})(1 - f\_{B\_1}) \\\\\\ = 1 - f\_{B\_1} - f\_{A\_1} - f\_{A\_1B\_1} - (1 - f\_{A\_1})(1 - f\_{B\_1}) \\\\\\ = 1 - f\_{B\_1} - f\_{A\_1} + f\_{A\_1B\_1} - 1 + f\_{B\_1} + f\_{A\_1} - f\_{A\_1}f\_{B\_1} \\\\\\ = f\_{A\_1B\_1} - f\_{A\_1}f\_{B\_1} = D\_{A\_1B\_1}$

 Similarly we can prove that $D\_{A\_1B\_1} = - D\_{A\_1B\_2} = - D\_{A\_2B\_1} = D\_{A\_2B\_2} = D$

This makes sense because linkage disequilibrium should be a measurement of two loci not any two specific alleles in those loci. Therefore the D for any haplotype between the two given loci should be the same (or at least the absolute value of it).
We then have:

> $D = D\_{A\_1B\_1} = f\_{A\_1B\_1} - f\_{A\_1}f\_{B\_1}$

> $D = -D\_{A\_1B\_2} = -f\_{A\_1B\_2} + f\_{A\_1}f\_{B\_2}$

> $D = -D\_{A\_2B\_1} = -f\_{A\_2B\_1} + f\_{A\_2}f\_{B\_1}$

> $D = D\_{A\_2B\_2} = f\_{A\_2B\_2} - f\_{A\_2}f\_{B\_2}$

Next we can prove that $D = f\_{A\_1B\_1}f\_{A\_2B\_2} - f\_{A\_1B\_2}f\_{A\_2B\_1}$:

> $f\_{A\_1B\_1}f\_{A\_2B\_2} \\\\\\ = (f\_{A\_1}f\_{B\_1} + D)(f\_{A\_2}f\_{B\_2} + D) \\\\\\ = f\_{A\_1}f\_{A\_2}f\_{B\_1}f\_{B\_2} + D(f\_{A\_1}f\_{B\_1} + f\_{A\_2}f\_{B\_2}) + D^2$

> $f\_{A\_1B\_2}f\_{A\_2B\_1} \\\\\\ = (f\_{A\_1}f\_{B\_2} - D)(f\_{A\_2}f\_{B\_1} - D) \\\\\\ = f\_{A\_1}f\_{A\_2}f\_{B\_1}f\_{B\_2} - D(f\_{A\_1}f\_{B\_2} + f\_{A\_2}f\_{B\_1}) + D^2$

Taske substraction:

> $f\_{A\_1B\_1}f\_{A\_2B\_2} - f\_{A\_1B\_2}f\_{A\_2B\_1} \\\\\\ = f\_{A\_1}f\_{A\_2}f\_{B\_1}f\_{B\_2} + D(f\_{A\_1}f\_{B\_1} + f\_{A\_2}f\_{B\_2}) + D^2 - (f\_{A\_1}f\_{A\_2}f\_{B\_1}f\_{B\_2} - D(f\_{A\_1}f\_{B\_2} + f\_{A\_2}f\_{B\_1}) + D^2) \\\\\\ = D(f\_{A\_1}f\_{B\_1} + f\_{A\_2}f\_{B\_2} + f\_{A\_1}f\_{B\_2} + f\_{A\_2}f\_{B\_1}) = D * 1 = D$

Now we have a measure of linkage disequilibrium. By definition, we know that $D=0$ indicates independent loci (no linkage). What should the maxium value of D be?

> Say we have a population with following genotype frequency:
  $f\_{A\_1} = f\_{A\_2} = 0.5 \\\\\\ f\_{B\_1} = f\_{B\_2} = 0.5$

> Suppose there is complete linkage between $A\_1$ and $B\_1$, meaning we have following haplotype frequencies:
  $f\_{A\_1B\_1} = f\_{A\_2B\_2} = 0.5 \\\\\\ f\_{A\_1B\_2} = f\_{A\_2B\_1} = 0$

> We can then calculate $D = f\_{A\_1B\_1}f\_{A\_2B\_2} - f\_{A\_1B\_2}f\_{A\_2B\_1} = 0.5 * 0.5 - 0 = 0.25$

When two loci are in complete linkage, we have $D=0.25$.
For any two loci, we always have $D \in [-0.25,0.25]$.

This scale is not very intuitive but we can work with it. Now next question is, does equal $D$ mean equal linkage disequilibrium?

> Consider the following two populations:

> 1. Pop 1 has haplotype frequencies as follow: $$f\_{A\_1B\_1} = f\_{A\_2B\_2} = 0.34 \\\\\\ f\_{A\_1B\_2} = f\_{A\_2B\_1} = 0.16$$
We can calculate $D = 0.34^2 - 0.16^2 = 0.09$
> 2. Pop 2 has haplotype frequencies as follow: $$f\_{A\_1B\_1} = 0.9 \\\\\\ f\_{A\_2B\_2} = 0.1 \\\\\\ f\_{A\_1B\_2} = f\_{A\_2B\_1} = 0$$
We can calculate $D = 0.9 * 0.1 - 0 = 0.09$

Even though $D$ at these loci for both populations is exactly the same, we can clearly see that pop 2 has comlete linkage between these two loci while pop 1 does not.

This example shows a major problem of $D$ for measuring linkage disequilibrium: It's ignorant of allele frequencies in a given population.

### Standardized Linkage Disequilibrium Coefficient ($D'$)

To address this problem, we can standardize $D$ against allele frequency:
  $$D' = \frac{D}{D_{max}}$$

$D\_{max}$ is the maxium possible $D$ in a population with same allele frequencies (but different haplotype frequencies). We have $$D\_{max} = f\_{maxA\_1B\_1} - f\_{A\_1}f\_{B\_1} \\\\\\ = min(f\_{A_1},f\_{B_1}) - f\_{A\_1}f\_{B\_1}$$
_We can also prove that for every haplotype between two given loci, we can get the same $D'$._

For example, in the above two populations:

  > 1. Pop 1: $$f\_{A\_1} = f\_{A\_2} = f\_{B\_1} = f\_{B\_2} = 0.5 \\\\\\ D\_{max} = 0.5 - 0.5 * 0.5 = 0.25 \\\\\\ D' = \frac{D}{D\_{max}} = \frac{0.09}{0.25} = \frac{9}{25} $$
  > 2. Pop 2: $$f\_{A\_1} = f\_{B\_1} = 0.9 \\\\\\ f\_{A\_2} = f\_{B\_2} = 0.1 \\\\\\ D\_{max} = 0.9 - 0.9 * 0.9 = 0.09 \\\\\\ D' = \frac{D}{D\_{max}} = \frac{0.09}{0.09} = 1$$

Now we can see that $D'$ for population 2 is much higher than that of population 1, indicating a much higher linkage disequilibrium between these loci in pop 2. By definition, we know $D' \in [0,1]$

However, $D'$ also has its own problem. Consider the following scenario:

  > Suppose we genotyped 100 individuals in a population, and count occurrance of each haplotype between loci A and B as follow:

||Count|Total|
|---|---|---|
|$A\_1B\_1$|50|100|
|$A\_1B\_2$|49|100|
|$A\_2B\_1$|0|100|
|$A\_2B\_2$|1|100|

> We can get haplotype and allele frequencies:
  $$f\_{A\_1B\_1} = 0.5, f\_{A\_1B\_2} = 0.49 \\\\\\ f\_{A\_2B\_1} = 0, f\_{A\_2B\_2} = 0.01 \\\\\\ f\_{A\_1} = 0.99, f\_{A\_2} = 0.01 \\\\\\ f\_{B\_1} = 0.5, f\_{B\_2} = 0.5$$
> And calculate $D'$:
  $$D' = \frac{f\_{A\_1B\_1} * f\_{A\_2B\_2} - f\_{A\_1B\_2} * f\_{A\_2B\_1}}{min(f\_{A\_1}, f\_{B\_1}) - f\_{A\_1}f\_{B\_1}} = \frac{0.5 * 0.01 - 0.49 * 0}{0.5 - 0.5 * 0.99} = 1$$

In this case, $D'$ indicates strong linkage between the two loci. However, looking at data, we can't confidently make any conclusions regarding the linkage between the two loci. The reason is that in all samples but one, they have either $A_1B_1$ or $A_1B_2$ haplotype. The only one that has an $A_2$ allele can simply be a result of a spontaneous mutaion rather than inheriting from a parent **We do not have enough information to say whether or not A locus is linked with B locus because $A\_2$ is mostly missing from data.**

In other words, $D'$ does not tell us how significant a linkage is or how confident we are in decalring a linkage disequilibrium. For this purpose, we turn to Pearson's correlation coefficient.

### Correlation coefficient ($\gamma^2$)

Consider the population above:

||Count|Total|
|---|---|---|
|$A\_1B\_1$|50|100|
|$A\_1B\_2$|49|100|
|$A\_2B\_1$|0|100|
|$A\_2B\_2$|1|100|

We calculated that $D=0.005$, now instead of  standardizing it like what we did with $D'$, we try a different approach:
  $$\gamma^2 = \frac{D^2}{f\_{A\_1}f\_{A\_2}f\_{B\_1}f\_{B\_2}}$$

We have $\gamma^2 = \frac{0.005^2}{0.99 * 0.01 * 0.5 * 0.5} = 0.01$

Now this seems to align well with our assessment of the data! As a matter of fact, this is actually the correlation coefficient of the two variables in this population!

Let's arbitratrily assign 1 to an $A_1$ allele and -1 to an $A_2$ allele. And 1 to $B_1$, -1 to $B_2$. Now we can plot the data and calculate $\gamma$:

{{< figure library="1" src="QE1_corrPlot.jpeg" title="Correlation plot" numbered="false" >}}

In the above plot we have $R=0.1$ this is exactly what we calculated above ($\gamma^2 = 0.01$)! Now that we have a correlation coefficient, we can use a $\chi^2$ test on our dataset:

  $$\chi_S^2=\gamma^2*N=0.01*100=1\\\\\\ P(\chi^2>\chi_S^2, df=1) = 0.317 $$

The p-value is also shown in the above plot. Clearly, we don't see a significant correlation (i.e linkage) between the two loci.

Now remember, **the absence of significance is NOT evidence of insignificance!** Look at the above figure and we notice that the confidence interval of the plot is very large towards $x=-1$. This is because we have only a single data point at $x=-1$. This could easily be a sampling error or like mentioned above, a spontaneous mutation. It is possible, that there are more individuals with $A_2$ allele but we just didn't include them in our samples for unknown reasons. In this case, since we can't estimate frequencies of $A_2$ in haplotype $A_2B_1$ or $A_2B_2$, we can't conclude with any confidence whether or not there is linkage between the two loci.
