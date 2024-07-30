const AWS = require('aws-sdk');
const dynamo = new AWS.DynamoDB.DocumentClient();

exports.handler = async (event) => {
    const params = {
        TableName: 'QuizTable',
        Key: { quizId: 'quiz1' }
    };

    const data = await dynamo.get(params).promise();
    const question = data.Item.questions[Math.floor(Math.random() * data.Item.questions.length)];

    return {
        statusCode: 200,
        body: JSON.stringify({
            question: question.text,
            answers: question.answers
        })
    };
};
