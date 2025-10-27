SRP
1. el orderProcessor tiene más de una responsabilidad. Sólo tendría que tener el processOrder y el validateOrder
2. el reportingEngine 

Open/closed
1. puede crecer en formas de hacer descuentos y eso haría que haya if/elses
2. acoplamiento muy alto


LSP
1. Un subtipo que no cumple el contrato no puede sustituir al tipo base.
2. el employee tiene el mismo método que el base. Tendrá clases duplicadas. Hace un override

ISP
1. 
2. 

DIP
1. debería implementar a databaseConnector así da igual que usas (sal, Mongo, etc)
2. 
