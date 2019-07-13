from PyQt5 import QtWidgets
from main import Ui_Form
import sys
class mywindow(QtWidgets.QMainWindow):
    def __init__(self):
        super(mywindow, self).__init__()
        self.ui = Ui_Form()
        self.ui.setupUi(self)
        self.ui.calculate.clicked.connect(self.avg)
        self.ui.addrow.clicked.connect(self.addorder)
        self.ui.clear.clicked.connect(self.clear)


    def avg(self):
         prvl =0
         totvol=0
         for price in range(self.ui.orders.rowCount()):
             if self.ui.orders.item(price, 0) is not None and self.ui.orders.item(price,1) is not None:
                prices,volume = (self.ui.orders.item(price, 0).text(),self.ui.orders.item(price,1).text())
                if self.checker(prices)==True and self.checker(volume) == True:
                   prvl = prvl + (float(prices) * float(volume))
                else:
                   QtWidgets.QMessageBox.about(self, "Input data error","Use only positive numbers and point ('.')  as divider, 8 digits after '.'")
                   break
             else:
                 QtWidgets.QMessageBox.about(self, "Input data error","All cells have to be filled")
                 break
         if prvl !=0:
           for vol in range(self.ui.orders.rowCount()):
                  volumes = float(self.ui.orders.item(vol,1).text())
                  totvol = totvol+volumes
           avg =  lambda prvl,totvol:prvl/totvol
           self.ui.avgp.setText(str('{:0.8f}'.format(round(avg(prvl,totvol),8))))
           self.ui.avgv.setText(str('{:0.8f}'.format(round(totvol,8))))

    def addorder(self):
        rc = self.ui.orders.rowCount()+1
        self.ui.orders.setRowCount(rc)

    def clear(self):
        self.ui.orders.setRowCount(2)
        for row in range(self.ui.orders.rowCount()):
            self.ui.orders.setItem(row, 0,None)
            self.ui.orders.setItem(row, 1, None)

    def checker(self,data):
        allowed = ('0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '.')
        good = True
        for x in data:
            if x not in allowed:
                good = False
                break
        if '.' in data and (len(data.split('.')[1])) > 8:
            good = False
        return (good)

app = QtWidgets.QApplication([])
application = mywindow()
application.show()

sys.exit(app.exec())
