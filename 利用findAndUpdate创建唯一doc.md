## 需求说明
- 假设名字唯一的doc只能有一个，利用new 创建的时候因为对name没有判断，导致name一样的doc插入多个

- 利用 findOneAndUpdate进行创建


```
  const saveDoctor = await Doctor.Model.findOneAndUpdate({
    _id: req.body._id || new mongoose.Types.ObjectId(),
  }, {
    $set: {
      name: req.body.name,
      mobile: req.body.mobile,
      department: req.body.department,
      title: req.body.title,
      headimageurl: req.body.headimageurl,
      description: req.body.description,
      hospital: hospital._id,
      gender: req.body.gender || 1,
    },
  }, {
    upsert: true,
    new: true,
    setDefaultsOnInsert: true,
  });
```
