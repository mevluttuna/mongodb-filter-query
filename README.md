# mongodb-filter-query
MongoDB data filter on document sub data list with multiple select.

```javascript

router.post('/get-filtered-data', async (req, res) => {
    try {
        // NOTE: Params
        const { userId, userEventStatus } = req.body

        // NOTE: Filter
        let users = (await Model.find({ user: mongoose.Types.ObjectId(userId), userEventStatus }))

        // NOTE: Mapped User Data List
        users = users.map(q => String(q.eventId))

        // NOTE: Filter Data by Users List
        const response = await OtherModel.find().where('_id').in(users).select()

        // NOTE: Return Response
        res.send(response);
    } catch (error) {
        // NOTE: Return Server Error with Message
        res.status(500).send(customError(error.message))
    }
})

```
