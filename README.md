im = np.zeros((3929,128,128))
mask = np.zeros((3929,128,128))
cntimg = 0
cntmask = 0
t=0
tempdir= filedialog.askdirectory(parent=root,initialdir='C:/Users/manes/Desktop/e-brain/Projects/Brain_Tumor_Seg/data')
file1=os.listdir(tempdir)
#print(tempdir)
#print(file1)
l1=len(file1)
print(l1)
t = 0
for k in range(0,l1):
    print(k)
    file=(os.path.join(tempdir,file1[k]))
    #print(file)
    file2 = os.listdir(file)
    for i in range(len(file2)):
        temp1 = np.array(plt.imread(os.path.join(file,file2[i])))
        temp=cv2.resize(temp1,(128,128))
        ndims = temp.ndim
        if ndims ==3:
            temp = cv2.cvtColor(temp,cv2.COLOR_BGR2GRAY)
            im[cntimg] = temp
            cntimg+=1
        else:
            indx,indy = np.where(temp != 0)
            temp[indx,indy] = 1
            mask[cntmask]=temp
            cntmask+=1

print(cntimg,cntmask)
